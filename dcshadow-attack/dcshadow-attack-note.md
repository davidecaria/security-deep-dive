# DCShadow attack description

## Concepts

- Active Directory
- MITRE ATT&CK Framework
- DCShadow

## Overview

A DC Shadow attack is a technique used by attackers to introduce a rogue domain controller into an Active Directory (AD) environment. This rogue DC replicates with legitimate domain controllers, allowing attackers to make unauthorized changes to AD data, including user permissions and security policies. This attack is designed to be stealthy and difficult to detect, making it a serious threat to AD security. The attack leverages the AD replication process, exploiting it to silently manipulate the directory. This attack is mapped on the MITRE ATT&CK framework as "Defence Evasion."

## Working principle

The DC Shadow attack is based on the common replication method of the Domain Controllers. The synch is used to stay updated on the changes in the directory. Inserting a rouge DC allows the attacker to poison the replication process and manipulate the data that are shared among DCs. A key aspect is that the rouge DC is kept under the radar and does not appear in the forest. This gains the attacker visibility and control even after having performed the attack and makes it harder to detect it. 

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

### Attack flow

Naming:

- Attacker = Oscar
- Domain controler = DC
- Privileged user = Alice
- Normal user = Bob

Settings:

Alice and Bob are users in the directory with different access levels. Oscar needs administrative access to perform a DC Shadow attack

Alice and Bob are users in the directory and have access to various resources in the network. Among them, the share access to a VM which would not necessary require privilege access, yet, both Alice and Bob access with their accoutns. Oscar would like to perform a DCShadow attack to alter the data shared in the replication process and gain control over the directory. Oscar has compromized Bob's account and got access to the VM where Alice and Bob work some time to time.

Flow:

1. Oscar is able to obtain the hash of Alice's password by dumping the predentials on the machine.
2. Oscar performs a Pass-The-Hash(PtH) and uses the retrived hash to issue a Kerberos TGT request.
3. The Key Distribution Center (KDC) issues a Ticket since the username and hash of the password match.
4. Oscar can set up a rounge DC that will be joined to the directory forest later on.
5. Oscar manipulates AD data, such as modifying user permissions or creating backdoor accounts.
6. Oscar maintains access by keeping the rogue DC operational and hidden.

### Example of the attack

1. Initial Compromise: Oscar uses phishing to obtain credentials for a high-privilege account (e.g., Alice’s).
2. Deploy Rogue DC: Using mimikatz, Oscar sets up a rogue domain controller.
3. Replication and Changes: The rogue DC replicates with legitimate DCs, allowing Oscar to alter AD data stealthily.
4. Cover Tracks: The rogue DC operates without detection, making it hard for administrators to spot unauthorized changes

## Impact 

A successful DC Shadow attack can have severe consequences:

1. Complete Domain Compromise: Attackers gain full control over the AD environment by manipulating critical AD data and permissions.
    
2. Privilege Escalation: Attackers can escalate their privileges and access sensitive systems and data.
    
3. Data Manipulation: Unauthorized changes can lead to data breaches and loss of control.

4. Operational Disruption: Tampering with AD settings can disrupt services and impact business continuity.

5. Long-term Persistence: The rogue DC provides ongoing access, making it challenging to fully remove the attacker from the environment.