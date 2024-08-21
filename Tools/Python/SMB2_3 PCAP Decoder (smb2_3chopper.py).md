```python
#Author found here:
#https://0xb0b.gitbook.io/writeups/tryhackme/2024/block

import hashlib
import hmac
import argparse
import binascii

# stolen from impacket. Thank you all for your wonderful contributions to the community
try:
    from Cryptodome.Cipher import ARC4
    from Cryptodome.Cipher import DES
    from Cryptodome.Hash import MD4
except Exception as e:
    print("Warning: You don't have any crypto installed. You need pycryptodomex")
    print("See https://pypi.org/project/pycryptodomex/")
    raise e

def generate_encrypted_session_key(key_exchange_key, exported_session_key):
    cipher = ARC4.new(key_exchange_key)
    cipher_encrypt = cipher.encrypt
    session_key = cipher_encrypt(exported_session_key)
    return session_key

parser = argparse.ArgumentParser(description="Calculate the Random Session Key based on data from a PCAP (maybe).")
parser.add_argument("-u", "--user", required=True, help="User name")
parser.add_argument("-d", "--domain", required=True, help="Domain name")
parser.add_argument("-p", "--password", help="Password of User")
parser.add_argument("-ph", "--passwordhash", help="NTLM Hash of the Password (in Hex)")
parser.add_argument("-n", "--ntproofstr", required=True, help="NTProofStr. This can be found in PCAP (provide Hex Stream)")
parser.add_argument("-k", "--key", required=True, help="Encrypted Session Key. This can be found in PCAP (provide Hex Stream)")
parser.add_argument("-v", "--verbose", action="store_true", help="Increase output verbosity")

args = parser.parse_args()

# Validate that either password or password hash is provided
if not args.password and not args.passwordhash:
    parser.error("You must provide either --password or --passwordhash")

# Upper Case User and Domain
user = str(args.user).upper().encode('utf-16le')
domain = str(args.domain).upper().encode('utf-16le')

# If password is provided, calculate the NTLM hash
if args.password:
    passw = args.password.encode('utf-16le')
    hash1 = hashlib.new('md4', passw)
    password_hash = hash1.digest()
else:
    # Use provided password hash (in hex) instead of calculating it
    password_hash = binascii.unhexlify(args.passwordhash)

# Calculate the ResponseNTKey
h = hmac.new(password_hash, digestmod=hashlib.md5)
h.update(user + domain)
resp_nt_key = h.digest()

# Use NTProofSTR and ResponseNTKey to calculate Key Exchange Key
nt_proof_str = binascii.unhexlify(args.ntproofstr)
h = hmac.new(resp_nt_key, digestmod=hashlib.md5)
h.update(nt_proof_str)
key_exch_key = h.digest()

# Calculate the Random Session Key by decrypting Encrypted Session Key with Key Exchange Key via RC4
r_sess_key = generate_encrypted_session_key(key_exch_key, binascii.unhexlify(args.key))

if args.verbose:
    print("USER WORK: " + user.decode('utf-16le') + domain.decode('utf-16le'))
    if args.password:
        print("PASS HASH: " + binascii.hexlify(password_hash).decode())
    print("RESP NT:   " + binascii.hexlify(resp_nt_key).decode())
    print("NT PROOF:  " + binascii.hexlify(nt_proof_str).decode())
    print("KeyExKey:  " + binascii.hexlify(key_exch_key).decode())
print("Random SK: " + binascii.hexlify(r_sess_key).decode())
```

