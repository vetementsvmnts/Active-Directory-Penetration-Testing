<div align="center">

```
 █████╗ ██████╗     ███████╗███╗   ██╗██╗   ██╗███╗   ███╗
██╔══██╗██╔══██╗    ██╔════╝████╗  ██║██║   ██║████╗ ████║
███████║██║  ██║    █████╗  ██╔██╗ ██║██║   ██║██╔████╔██║
██╔══██║██║  ██║    ██╔══╝  ██║╚██╗██║██║   ██║██║╚██╔╝██║
██║  ██║██████╔╝    ███████╗██║ ╚████║╚██████╔╝██║ ╚═╝ ██║
╚═╝  ╚═╝╚═════╝     ╚══════╝╚═╝  ╚═══╝ ╚═════╝ ╚═╝     ╚═╝
        A C T I V E   D I R E C T O R Y   E N U M E R A T I O N
```

**Systematic enumeration and attack-path mapping against a Windows Active Directory environment**

[![Active Directory](https://img.shields.io/badge/Active%20Directory-0078D4?style=for-the-badge&logo=windows&logoColor=white)](#)
[![BloodHound](https://img.shields.io/badge/BloodHound-1A1A1A?style=for-the-badge&logo=hackaday&logoColor=00FF41)](https://github.com/BloodHoundAD/BloodHound)
[![Impacket](https://img.shields.io/badge/Impacket-2E7D32?style=for-the-badge&logo=python&logoColor=white)](https://github.com/fortra/impacket)
[![License: MIT](https://img.shields.io/badge/License-MIT-00FF41?style=for-the-badge)](LICENSE)

</div>

---

## `~$ cat abstract.md`

This repository documents a full enumeration pass against a lab Active Directory domain, covering
unauthenticated recon, LDAP/SMB/RPC enumeration, Kerberos abuse, ACL-based attack-path discovery, and
trust/GPO mapping — building toward a complete picture of the domain's attack surface without touching
exploitation.

Each phase follows a consistent methodology: **discover → enumerate → correlate → map → report**, with
findings organized by enumeration technique and cross-referenced against MITRE ATT&CK where applicable.

---

## `~$ cat brief.md`

**Objective:** Enumerate a Windows Active Directory domain from an unauthenticated and low-privilege
foothold to fully map users, groups, computers, trusts, GPOs, and ACL relationships — surfacing viable
privilege-escalation paths to Domain Admin.

**Environment:** Lab AD domain (Windows Server DC + joined workstations), enumerated from an attacker-controlled
Kali host — no production infrastructure or real organizational data involved.

---

## `~$ ls phases/`

| # | Phase | Focus | Status |
|---|-------|-------|--------|
| 01 | Unauthenticated Recon | Domain/DC discovery, DNS, SMB null sessions | ⬜ |
| 02 | LDAP Enumeration | Users, groups, OUs, password policy, descriptions | ⬜ |
| 03 | SMB & RPC Enumeration | Shares, sessions, RID cycling, local groups | ⬜ |
| 04 | Kerberos Enumeration | AS-REP roasting, Kerberoasting, user validation | ⬜ |
| 05 | BloodHound Collection | SharpHound ingestion, attack-path graphing | ⬜ |
| 06 | ACL & Object Abuse Mapping | DACL/ACE abuse chains, dangerous delegations | ⬜ |
| 07 | Trusts & GPO Enumeration | Domain/forest trusts, GPO misconfiguration review | ⬜ |
| 08 | Reporting | Findings writeup, path-to-DA narrative, remediation | ⬜ |

> Status updates as each phase is completed. Each row will link to a self-contained folder with its own
> README, evidence, and supporting scripts.

---

## `~$ cat structure.md`

```
AD-Enumeration/
├── 01-unauth-recon/            # DC discovery, DNS, null session findings
├── 02-ldap-enum/                # LDAP dumps, password policy, user/group data
├── 03-smb-rpc-enum/             # Share listings, RID cycling, session enum
├── 04-kerberos-enum/            # AS-REP/Kerberoast hashes, validated userlists
├── 05-bloodhound/               # SharpHound output, queries, path screenshots
├── 06-acl-abuse-mapping/        # ACE abuse chains, delegation findings
├── 07-trusts-gpo/               # Trust map, GPO misconfig findings
├── 08-reporting/                # Final writeup + remediation notes
├── images/                      # Screenshots / evidence
├── README.md                    # This file — master index
└── LICENSE
```

---

## `~$ cat methodology.md`

- **Unauthenticated Recon** — DNS zone checks, DC identification, SMB null/anonymous session testing to establish an initial foothold-free view of the domain
- **LDAP Enumeration** — Full user/group/OU dump via `ldapsearch`, password policy extraction, mining `description` fields for leaked credentials
- **SMB & RPC Enumeration** — Share and session enumeration, RID cycling for user/group discovery on hosts with weak ACLs
- **Kerberos Enumeration** — AS-REP roasting against accounts with pre-auth disabled, Kerberoasting of SPN-linked service accounts, username validation via Kerberos pre-auth timing
- **BloodHound Collection** — SharpHound ingestion of sessions, ACLs, group memberships, and trusts, graphed for shortest-path-to-DA analysis
- **ACL & Object Abuse Mapping** — Identifying abusable ACEs (GenericAll, WriteDACL, ForceChangePassword, etc.) and unconstrained/constrained delegation misconfigurations
- **Trusts & GPO Enumeration** — Mapping domain/forest trust relationships and reviewing GPOs for exploitable misconfigurations
- **Reporting** — Consolidated findings, a narrative path-to-Domain-Admin writeup, and remediation guidance per finding

---

## `~$ cat tools.md`

| Tool / Standard | Purpose |
|---|---|
| **BloodHound / SharpHound** | Attack-path graphing from collected AD relationship data |
| **Impacket suite** | GetNPUsers, GetUserSPNs, secretsdump, and other protocol-level enumeration |
| **CrackMapExec / NetExec** | Cross-protocol enumeration (SMB, LDAP, WinRM) and session validation |
| **enum4linux-ng** | SMB/RPC null-session enumeration |
| **Kerbrute** | Username enumeration and password spraying via Kerberos pre-auth |
| **ldapsearch / windapsearch** | Raw LDAP querying and directory dumps |
| **MITRE ATT&CK** | Technique mapping for enumeration and discovery findings |

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
