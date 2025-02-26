# More linux commands

"если не страдать этой херней которую и так знаешь то забудешь её в самый ответственнный момент на собесе"
 - джейсон стэтхем

## 1 / 10
Which user is current user on host01 server?

```
thor@host01 ~$ whoami 
thor
```

right answer - thor

## 2 / 10
What is id of thor user?

```
thor@host01 ~$ id
uid=1001(thor) gid=1001(thor) groups=1001(thor),10(wheel)
```

right answer - 1001

## 3 / 10
Which command you will use to switch to ansible user?

```
su ansible
```

## 4 / 10
Which command you will use to login to other server with IP 172.16.238.3 and thor user?

```
ssh thor@172.16.238.3
```

## 5 / 10
Which of the following file is present under /root directory?
Note: Normal user don't have permission to view files under /root directory so you will have to gain higher privileges to see files under /root.

```
thor:x:1001:1001::/home/thor:/bin/bash
thor@host01 ~$ sudo ls -la /root
total 60
dr-xr-x--- 1 root root 4096 Feb 26 12:01 .
drwxr-xr-x 1 root root 4096 Feb 26 12:01 ..
-rw-r--r-- 1 root root   18 Aug 10  2021 .bash_logout
-rw-r--r-- 1 root root  141 Aug 10  2021 .bash_profile
-rw-r--r-- 1 root root  518 Feb 18 11:50 .bashrc
-rw-r--r-- 1 root root  100 Aug 10  2021 .cshrc
drwx------ 1 root root 4096 Feb 26 12:01 .ssh
-rw-r--r-- 1 root root  129 Aug 10  2021 .tcshrc
drwx------ 2 root root 4096 Feb 26 12:01 .terminal_logs
-rw------- 1 root root 4115 Jul  8  2024 anaconda-ks.cfg
-rw------- 1 root root   95 Jul  8  2024 anaconda-post-nochroot.log
-rw------- 1 root root  435 Jul  8  2024 anaconda-post.log
-rw------- 1 root root 3850 Jul  8  2024 original-ks.cfg
```

right answer - anaconda-ks.cfg

## 6 / 10
Which command can't be used to download file over internet?

right answer - ping

## 7 / 10
Download target file to host01
target file name : dummy.pdf
target file URL: https://www.w3.org/WAI/ER/tests/xhtml/testfiles/resources/pdf/dummy.pdf
target directory: /home/thor

```
thor@host01 ~$ pwd
/home/thor
thor@host01 ~$ wget https://www.w3.org/WAI/ER/tests/xhtml/testfiles/resources/pdf/dummy.pdf
--2025-02-26 12:11:58--  https://www.w3.org/WAI/ER/tests/xhtml/testfiles/resources/pdf/dummy.pdf
Resolving www.w3.org (www.w3.org)... 104.18.23.19, 104.18.22.19, 2606:4700::6812:1713, ...
Connecting to www.w3.org (www.w3.org)|104.18.23.19|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 13264 (13K) [application/pdf]
Saving to: ‘dummy.pdf’

dummy.pdf                        100%[========================================================>]  12.95K  --.-KB/s    in 0s      

2025-02-26 12:12:03 (135 MB/s) - ‘dummy.pdf’ saved [13264/13264]

thor@host01 ~$ ls -la | grep dum
-rw-r--r-- 1 thor thor 13264 Aug 27  2007 dummy.pdf
```

##  8 / 10
Where can you find OS information of linux servers?

right answer - /etc/*release*

## 9 / 10
Which OS is running on host01 server?

```
thor@host01 ~$ cat /etc/os-release 
NAME="CentOS Stream"
VERSION="9"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="9"
PLATFORM_ID="platform:el9"
PRETTY_NAME="CentOS Stream 9"
ANSI_COLOR="0;31"
LOGO="fedora-logo-icon"
CPE_NAME="cpe:/o:centos:centos:9"
HOME_URL="https://centos.org/"
BUG_REPORT_URL="https://issues.redhat.com/"
REDHAT_SUPPORT_PRODUCT="Red Hat Enterprise Linux 9"
REDHAT_SUPPORT_PRODUCT_VERSION="CentOS Stream"
```

right answer - "CentOS"

## 10 / 10
Which version of CentOS is running on host01 server?

right answer - 9 (see prev stdout)

