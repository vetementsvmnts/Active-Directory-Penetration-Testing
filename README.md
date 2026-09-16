<div align="center">

```
 █████╗ ██████╗     ██████╗ ███████╗███╗   ██╗████████╗███████╗███████╗████████╗
██╔══██╗██╔══██╗    ██╔══██╗██╔════╝████╗  ██║╚══██╔══╝██╔════╝██╔════╝╚══██╔══╝
███████║██║  ██║    ██████╔╝█████╗  ██╔██╗ ██║   ██║   █████╗  ███████╗   ██║   
██╔══██║██║  ██║    ██╔═══╝ ██╔══╝  ██║╚██╗██║   ██║   ██╔══╝  ╚════██║   ██║   
██║  ██║██████╔╝    ██║     ███████╗██║ ╚████║   ██║   ███████╗███████║   ██║   
╚═╝  ╚═╝╚═════╝     ╚═╝     ╚══════╝╚═╝  ╚═══╝   ╚═╝   ╚══════╝╚══════╝   ╚═╝   
              A C T I V E   D I R E C T O R Y   P E N T E S T I N G
```

**End-to-end offensive assessment of a Windows Active Directory environment — foothold to domain dominance**

[![Active Directory](https://img.shields.io/badge/Active%20Directory-0078D4?style=for-the-badge&logo=windows&logoColor=white)](#)
[![BloodHound](https://img.shields.io/badge/BloodHound-1A1A1A?style=for-the-badge&logo=hackaday&logoColor=00FF41)](https://github.com/BloodHoundAD/BloodHound)
[![Impacket](https://img.shields.io/badge/Impacket-2E7D32?style=for-the-badge&logo=python&logoColor=white)](https://github.com/fortra/impacket)
[![MITRE ATT&CK](https://img.shields.io/badge/MITRE%20ATT%26CK-1A1A1A?style=for-the-badge&logoColor=00FF41)](https://attack.mitre.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-00FF41?style=for-the-badge)](LICENSE)

</div>

---

## `~$ cat abstract.md`

This repository documents a full offensive engagement against a lab Active Directory domain — from an initial
unauthenticated foothold through enumeration, credential attacks, lateral movement, privilege escalation, and
full domain compromise. Each stage is treated as a discrete, evidenced phase of the kill chain rather than a
single walkthrough, with techniques mapped to MITRE ATT&CK and findings framed the way they'd appear in a
client-facing report.

Methodology throughout: **recon → exploit → escalate → pivot → dominate → report**, with every technique
validated against a live domain controller and joined hosts in an isolated lab.

---

## `~$ cat brief.md`

**Objective:** Simulate a real-world adversary against a Windows Active Directory environment — starting from
an assumed-breach or unauthenticated position — to obtain Domain Admin, demonstrate business impact, and
deliver actionable remediation guidance.

**Environment:** Lab AD domain (Windows Server DC + joined workstations, multiple simulated user tiers),
attacked from a Kali host — no production infrastructure, real organizational data, or unauthorized targets
involved.



## `~$ cat structure.md`

```
AD-Pentesting/
├── 01-recon-enum/               # Domain/DC discovery, LDAP/SMB/RPC enumeration
├── 02-initial-foothold/         # Spraying, AS-REP roasting, poisoning captures
├── 03-credential-access/        # Kerberoast hashes, cracked creds, dumped secrets
├── 04-local-privesc/            # Host-level privilege escalation notes + evidence
├── 05-lateral-movement/         # PtH/PtT logs, pivot paths, session evidence
├── 06-domain-privesc/           # ACL/delegation/GPO abuse chains
├── 07-domain-dominance/         # DCSync output, ticket forging, persistence
├── 08-defense-evasion/          # Evasion techniques + detection notes
├── 09-reporting/                # Final report, attack narrative, remediation
├── images/                      # Screenshots / evidence
├── README.md                    # This file — master index
└── LICENSE
```

---

## `~$ cat methodology.md`

- **Recon & Enumeration** — Unauthenticated and low-privilege enumeration of the domain (LDAP, SMB, RPC, DNS) to map users, groups, computers, and initial attack surface
- **Initial Foothold** — Password spraying against validated usernames, AS-REP roasting of pre-auth-disabled accounts, and LLMNR/NBT-NS/mDNS poisoning for credential capture
- **Credential Access** — Kerberoasting SPN-linked service accounts, offline hash cracking, and credential/secret dumping from compromised hosts
- **Local Privilege Escalation** — Exploiting host-level misconfigurations (service permissions, stored credentials, token abuse) to gain SYSTEM/root on footholds
- **Lateral Movement** — Pass-the-hash and pass-the-ticket to pivot between hosts, session hunting to locate high-value credentials
- **Domain Privilege Escalation** — Abusing ACLs/ACEs (GenericAll, WriteDACL, ForceChangePassword), delegation misconfigurations, and GPO permissions to climb toward Domain Admin
- **Domain Dominance** — DCSync for full credential extraction, Golden/Silver Ticket forging, and persistence mechanisms (AdminSDHolder, skeleton key, etc.) demonstrating full compromise
- **Defense Evasion & Detection** — Notes on evasion of AV/EDR controls encountered, and observations on what activity would have been logged/detected
- **Reporting** — Consolidated findings, a narrative attack chain from foothold to Domain Admin, risk ratings, and remediation guidance per finding

---

## `~$ cat tools.md`

| Tool / Standard | Purpose |
|---|---|
| **BloodHound / SharpHound** | Attack-path graphing and shortest-path-to-DA analysis |
| **Impacket suite** | GetNPUsers, GetUserSPNs, secretsdump, psexec.py, wmiexec.py |
| **CrackMapExec / NetExec** | Cross-protocol enumeration, spraying, and lateral movement |
| **Responder** | LLMNR/NBT-NS/mDNS poisoning for credential capture |
| **Mimikatz / Rubeus** | In-memory credential extraction, ticket forging and manipulation |
| **Hashcat** | Offline cracking of captured/roasted hashes |
| **PowerView / PowerSploit** | AD object and ACL enumeration from a Windows context |
| **Kerbrute** | Username enumeration and password spraying via Kerberos pre-auth |
| **MITRE ATT&CK** | Technique mapping across the full kill chain |

---

## `~$ contact --info`

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](#)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/vetementsvmnts)

---

<div align="center">

*This engagement was conducted entirely against an isolated lab Active Directory domain for educational and
portfolio purposes only. No production infrastructure, real organizational data, or unauthorized targets were
involved.*

</div>
