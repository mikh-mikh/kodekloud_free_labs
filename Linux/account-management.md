# kodekloud free labs linux account managment

You teach best what you most need to learn.

– Richard Bach

## 1 / 11
info
This lab requires some commands to be run as the root user. Always use sudo.

Bob's default password is caleston123

yes, boss

## 2 / 11
What type of account does Bob use?

```
bob@caleston-lp10:~$ id bob
uid=1000(bob) gid=1000(bob) groups=1000(bob)
bob@caleston-lp10:~$ cat /etc/passwd | grep bob
bob:x:1000:1000::/home/bob:/bin/bash
```

right answer - "user account"

## 3 / 11

Which of the following commands will show you the UID for a user?
If unsure, try out the commands in the terminal and find the answer!

ну ёк макарек, смотрели же ранее

right answer - "id"

## 4 / 11
What is the UID for bob?

ну спросили бы раньше ж:)

right answer - "1000" (see.prev. stdout)

## 5 / 11

What level of sudo access does bob have in this system?

Боб не колесован, подозрительно

```
bob@caleston-lp10:~$ sudo cat /etc/sudoers          
#
# This file MUST be edited with the 'visudo' command as root.
#
# Please consider adding local content in /etc/sudoers.d/ instead of
# directly modifying this file.
#
# See the man page for details on how to write a sudoers file.
#
Defaults        env_reset
Defaults        mail_badpass
Defaults        secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin"

# Host alias specification

# User alias specification

# Cmnd alias specification

# User privilege specification
root    ALL=(ALL:ALL) ALL

# Members of the admin group may gain root privileges
bob ALL=(ALL) ALL

# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL

# See sudoers(5) for more information on "#include" directives:

#includedir /etc/sudoers.d
```

right answer - "ALL Permissions"

## 6 / 11
Which access control file has the encrypted password for the users?

right answer - "/etc/shadow" (а если доменный? ахахахах)

## 7 / 11

A user called chris has been created.
Can you find out his Full Name?

```
bob@caleston-lp10:~$ cat /etc/passwd | grep chris
chris:x:1002:1002:Chris Hunter:/home/chris:/bin/sh
```
GOTCHA

right answer - "Chris Hunter"

## 8 / 11
Which groups are chris part of?

```
bob@caleston-lp10:~$ id chris
uid=1002(chris) gid=1002(chris) groups=1002(chris),1003(cannon),1004(sapphire)
```

right answer - "chris, cannon, sapphire"

## 9 / 11
What is chris's primary group?

right answer - "chris"

## 10 / 11

Now, lets create a new user called sarah. Once done, set her password to caleston321

```
bob@caleston-lp10:~$ sudo useradd -m sarah
bob@caleston-lp10:~$ sudo passwd sarah
Enter new UNIX password: 
Retype new UNIX password: 
passwd: password updated successfully
```

## 11 / 11

Create a group called john with the GID 1010. Next create another user called john with UID = 1010, primary group = john and login shell = /bin/sh

```
bob@caleston-lp10:~$ sudo groupadd -g 1010 john
bob@caleston-lp10:~$ sudo useradd -m -g 1010 -u 1010 -s /bin/sh john
bob@caleston-lp10:~$ id john
uid=1010(john) gid=1010(john) groups=1010(john)
bob@caleston-lp10:~$ cat /etc/passwd | grep john
john:x:1010:1010::/home/john:/bin/sh
```

детский сад, все равно меня не возьмут на раюоту :)
