# kodekloud free labs linux - IPTABLES

Whatever we believe about ourselves and our ability comes true for us.

– Susan L. Taylor

## 1 / 8

In this Lab, we will secure the development environment by making use of iptables.
Wherever required, use sudo to run commands as the root user. Bob's password is caleston123.

okay

## 2 / 8

Here is the simple architecture diagram of the implementation. This is a two-tier application.

The web server is hosted on devapp01.
The DB server is hosted on devdb01.
The Software Repository is hosted on caleston-repo-01.

Here are the connectivity requirements:

SSH should be allowed from Bob's laptop to both Web and DB servers.
HTTP/80 from the Web Server should be accessible from Bob's laptop.
The Web Server should be able to access the Software Repository server at port 80

На схемке лэптоб Боба в одном контуре, и в другом 3 машины: веб, бд и репа. у боба сетевые доступа (исходящие) 80/22 до вебсервера и 22 до БД. 
у вебсервера до БД 5432 исходящий (синий слоник) и 80 исходящий до репы

okay

## 3 / 8
Install iptables on devapp01 and devdb01 servers (а репа? наверное нельзя туда Бобу)

ну три машины, зачем городить что то, делаем на каждой:
```
sudo apt update && sudo apt install -y iptables
```

## 4 / 8
Are there any iptable rules created on either Web Server or DB Server right now?
конечно же нет

right answer - NO

## 5 / 8

On devapp01, add an incoming rule permitting SSH and HTTP connection from Bob's Laptop.
Bob's Laptop has an IP address of 172.16.238.187

```
bob@devapp01:~$ sudo iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
bob@devapp01:~$ sudo iptables -A INPUT -p tcp -s 172.16.238.187 --dport 22 -j ACCEPT
bob@devapp01:~$ sudo iptables -A INPUT -p tcp -s 172.16.238.187 --dport 80 -j ACCEPT
bob@devapp01:~$ sudo iptables -P INPUT DROP
bob@devapp01:~$ sudo iptables -L
Chain INPUT (policy DROP)
target     prot opt source               destination         
ACCEPT     tcp  --  caleston-lp10        anywhere             tcp dpt:ssh
ACCEPT     tcp  --  caleston-lp10        anywhere             tcp dpt:http
ACCEPT     all  --  anywhere             anywhere             ctstate RELATED,ESTABLISHED

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination         

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination
```

## 6 / 8

Now, lockdown incoming traffic on devapp01. Drop incoming connections from any source on any destination port for any protocol (TCP/UDP).
Remember, this rule should be at the bottom of the chain for the SSH and HTTP access from caleston-lp10 to work.

did it early
ругается проверятор заданий - DROP хочет в конце цепочки хотя он полиси по умолчанию - ну ладно
```
sudo iptables -A INPUT -j DROP
```

## 7 / 8

On devapp01, add an outgoing rule permitting access to port 5432 on devdb01 and HTTP access to caleston-repo-01. 
Once this is done, block outgoing traffic to any destination on http/https ports from devapp01
Note: caleston-repo-01 has the ip address of 172.16.238.15

devdb01 ip = 172.16.238.11

```
bob@devapp01:~$ sudo iptables -A OUTPUT -p tcp -d 172.16.238.15 --dport 80 -j ACCEPT
bob@devapp01:~$ sudo iptables -A OUTPUT -p tcp -d 172.16.238.15 --dport 443 -j ACCEPT
bob@devapp01:~$ sudo iptables -A OUTPUT -p tcp -d 172.16.238.11 --dport 5432 -j ACCEPT
bob@devapp01:~$ sudo iptables -A OUTPUT -p tcp --dport 443 -j DROP  
bob@devapp01:~$ sudo iptables -A OUTPUT -p tcp --dport 80 -j DROP
bob@devapp01:~$ sudo iptables -L                                 
Chain INPUT (policy DROP)
target     prot opt source               destination         
ACCEPT     all  --  anywhere             anywhere             ctstate RELATED,ESTABLISHED
ACCEPT     tcp  --  caleston-lp10        anywhere             tcp dpt:ssh
ACCEPT     tcp  --  caleston-lp10        anywhere             tcp dpt:http            
DROP       all  --  anywhere             anywhere            

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination         

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination         
ACCEPT     tcp  --  anywhere             caleston-repo-01     tcp dpt:http
ACCEPT     tcp  --  anywhere             caleston-repo-01     tcp dpt:https
ACCEPT     tcp  --  anywhere             devdb01              tcp dpt:postgresql
DROP       tcp  --  anywhere             anywhere             tcp dpt:https
DROP       tcp  --  anywhere             anywhere             tcp dpt:http
```

## 8 / 8
Add an OUTPUT rule to the top of the chain which will allow https connection to google.com on devapp01

```
bob@devapp01:~$ sudo iptables -I OUTPUT 1 -p tcp -d google.com --dport 443 -j ACCEPT
bob@devapp01:~$ sudo iptables -L OUTPUT --line-numbers
Chain OUTPUT (policy ACCEPT)
num  target     prot opt source               destination         
1    ACCEPT     tcp  --  anywhere             google.com           tcp dpt:https
2    ACCEPT     tcp  --  anywhere             caleston-repo-01     tcp dpt:http
3    ACCEPT     tcp  --  anywhere             caleston-repo-01     tcp dpt:https
4    ACCEPT     tcp  --  anywhere             devdb01              tcp dpt:postgresql
5    DROP       tcp  --  anywhere             anywhere             tcp dpt:https
6    DROP       tcp  --  anywhere             anywhere             tcp dpt:http
bob@devapp01:~$ wget https://google.com
--2025-03-03 06:36:45--  https://google.com/
Resolving google.com (google.com)... 173.194.194.101
Connecting to google.com (google.com)|173.194.194.101|:443... connected.
HTTP request sent, awaiting response... 301 Moved Permanently
```

curl нетуть:)

а зачем мы только вебсервер настраивали, а БД? 
а наш лэптоп в "закрытом контуре" был нарисован - а он в той же сети что эти тачки
