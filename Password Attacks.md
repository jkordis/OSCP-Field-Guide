| **Tool/Category** | **Purpose** | **Command Examples** | **Notes** |
| --- | --- | --- | --- |
| **John the Ripper** |  |  |  |
| Basic Password Cracking | Crack a password hash using a wordlist. | `john --wordlist=/path/to/wordlist.txt <hashfile>` | Supports multiple hash formats; use `--format=<format>` to specify. |
| Identify Hash Format | Automatically detect hash type. | `john --show --format=auto <hashfile>` | Useful to ensure proper cracking mode. |
| Resume Cracking Session | Resume a previously interrupted cracking session. | `john --restore` | Restores from the saved session file. |
| Incremental Mode | Attempt password cracking with brute force. | `john --incremental <hashfile>` | Use when no wordlist is available. |
| **Hashcat** |  |  |  |
| Basic Password Cracking | Crack a hash using a wordlist. | `hashcat -m <hash_type> -a 0 <hashfile> /path/to/wordlist.txt` | Replace `<hash_type>` with appropriate code (e.g., 0 for MD5, 1000 for NTLM). |
| Brute Force Attack | Attempt all possible combinations of a given charset. | `hashcat -m <hash_type> -a 3 <hashfile> ?a?a?a?a` | Replace `?a` with desired charset (`?l` for lowercase, `?u` for uppercase, etc.). |
| Mask Attack | Crack with patterns (e.g., passwords ending in numbers). | `hashcat -m <hash_type> -a 3 <hashfile> password?d?d` | Use masks for predictable patterns (e.g., `password12`). |
| Rule-Based Attack | Apply rules to mutate words in a wordlist. | `hashcat -m <hash_type> -a 0 <hashfile> /path/to/wordlist.txt -r /path/to/rules.rule` | Default rules like `rockyou-30000.rule` are common. |
| **Hydra** |  |  |  |
| Brute Force SSH | Attempt SSH login with a username and password list. | `hydra -l <username> -P /path/to/password_list.txt ssh://<target>` | Replace `-l` with `-L /path/to/userlist.txt` for multiple usernames. |
| HTTP Login Attack | Attempt login to an HTTP form. | `hydra -l <username> -P /path/to/password_list.txt <target> http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect"` | Adjust parameters based on the login form structure. |
| SMB Brute Force | Brute force SMB credentials. | `hydra -L /path/to/userlist.txt -P /path/to/password_list.txt smb://<target>` | Useful for Windows-based SMB services. |
| FTP Brute Force | Test FTP credentials. | `hydra -l <username> -P /path/to/password_list.txt ftp://<target>` | Many FTP servers allow anonymous login (`hydra -l anonymous`). |
| **Other Useful Tools** |  |  |  |
| CeWL | Generate a custom wordlist from website content. | `cewl -d 3 -m 5 -w wordlist.txt <website>` | Adjust depth (`-d`) and minimum word length (`-m`) based on the target. |
| Crunch | Generate a wordlist based on specific parameters. | `crunch 8 8 abc123 -o wordlist.txt` | Generates all combinations of `abc123` with length 8. |
| Medusa | Fast login brute forcer for various protocols. | `medusa -h <target> -u <username> -P /path/to/password_list.txt -M ssh` | Replace `ssh` with desired module (e.g., `ftp`, `http`). |
| Wordlists | Prebuilt collections of passwords for cracking. | Example files: `/usr/share/wordlists/rockyou.txt`, `/usr/share/wordlists/fasttrack.txt` | Rockyou is commonly used for dictionary attacks.  SecLists also has a lot of common passwords to use |
|  |  |  |  |
