### Intruder
[[Web Basics]] 

| **Attack**    | **Postions/Payloads** | **Operation**                                                                                                                                 | **Use Case**                                                                                    |
| ------------- | --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| Pitchfork     | Multiple Up to 20     |                                                                                                                                               | Credential Stuffing                                                                             |
| Cluster Bomb  | Multiple Up to 20     | Tests every combination between payload sets. IE: User_List and Pass_List<br><br>Joe: Joe<br><br>Joe: Dude<br><br>Brad: Joe<br><br>Brad: Dude | credential brute-forcing scenarios where the mapping between usernames and passwords is unknown |
| Battering Ram | 1                     | Same Payload all positions simultaneously                                                                                                     | Default Credential Fuzz                                                                         |
| Sniper        | 1                     | Iterate Payload into Position                                                                                                                 | Password Brute-Force/ API Endpoint Fuzzing                                                      |

### Repeater


### Sequencer
Helpful for identifying the strength of session token and **C**ross-**S**ite **R**equest **F**orgery (CSRF) tokens randomness in token.

We could predict upcoming token values

### Decoder

### Extensions
Jython - Allows running python extensions/modules through Burp