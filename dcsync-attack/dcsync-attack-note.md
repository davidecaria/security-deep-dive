# DCSync attack description

## Concepts

- Active Directory
- MITRE ATT&CK Framework
- DCSync

## Overview

A DCSync attack is a technique used by attackers to impersonate a domain controller and retrieve sensitive information from Active Directory, specifically user credentials and password hashes. As a consequence of this attack, an adversary can escalate privileges and move laterally in the network. The attack leverages the Directory Replication Service (DRS) Remote Protocol (MS-DRSR) used by domain controllers in Active Directory (AD) to synchronize data. By exploiting this replication protocol, an attacker with sufficient privileges can force this replication to obtain sensitive information.

## Working principle

The DCSync attack leverages a commonly used protocol in Active Directory: Directory Replication Service (DRS) Remote Protocol (MS-DRSR). This protocol is used by Domain Controllers to replicate directory data and synchronize with other elements of the directory. This is a standard procedure that ensures Domain Controllers and other elements of the directory are synchronized and aligned. From the point of view of an attacker, the objective is to gain sufficient privileges to trigger this protocol and retrieve password hashes. Those hashes can then be used to obtain Kerberos Ticket Granting Tickets (TGT) and proceed with lateral movement and privilege escalation in the targeted environment. This attack is mapped on the MITRE ATT&CK framework as "Credential Access."

### Compromise a privileged account

To start the attack, an adversary would need to gain access to a privileged account in the directory, namely, a member of the Domain Admins, Enterprise Admins, or a user that has Replication-Get-Changes-All permissions.

There are various options for an attacker to gain such privilege access:

- Phishing attacks 
The attacker can trick a sufficiently privileged user into giving up their credentials.
- Exploiting SW Vulnerabilities
The attacker may exploit known vulnerabilities in legacy applications to gain unauthorized access to credentials.
- Brute force
The attacker may be able to brute force weak passwords to gain unauthorized access.
- Pass-the-Hash
If the attacker has previously obtained the hash of a password, it can be used to authenticate further
- Credentail dumping
The attacker may dump credentials on machines where administrators or privileged accounts have access

### Example of the attack

1. Initial Compromise: The attacker uses phishing to gain credentials for a regular user account.
2. Credential Dumping: Using Mimikatz, the attacker dumps credentials from the compromised user's machine.
3. Lateral Movement: With the obtained credentials, the attacker moves laterally within the network, targeting systems used by higher-privilege users.
4. Privilege Escalation: The attacker finds a machine used by a member of the Domain Admins group, dumps the credentials, and obtains a Domain Admin hash.
5. Performing DCSync: Using Mimikatz with the Domain Admin credentials, the attacker executes a DCSync attack to replicate and retrieve password hashes for the entire domain.

## Impact

A successful DCSync attack can have severe consequences for an organization:

1. Complete Domain Compromise: By retrieving password hashes for any user in the domain, including highly privileged accounts like Domain Admins, an attacker can gain full control over the entire Active Directory environment.

2. Lateral Movement: With the obtained credentials, attackers can move laterally across the network, accessing sensitive systems and data, and escalating their privileges further.

3. Data Theft: Attackers can exfiltrate sensitive information, including personal data, intellectual property, and financial records, leading to significant data breaches.

4. Service Disruption: Attackers can disrupt operations by tampering with Active Directory services, causing downtime and impacting business continuity.

5. Long-term Persistence: By maintaining access to highly privileged accounts, attackers can establish persistent backdoors in the network, making it difficult to completely remove their presence and secure the environment.


