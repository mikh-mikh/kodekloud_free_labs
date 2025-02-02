#DNS

## If you can't explain it simply you don't understand it well enough.

– Albert Einstein
##

### At basic level what is DNS used for ?

to resolve domain name of an IP
to resolve IP of a domain name +
to connect a system with internet
to enable networking on a system

### On a Linux based system, which of the following file can be used to point domains/hostnames to IPs locally?

/etc/resolv.conf
/etc/hosts +
/etc/host
/etc/hostname

### On a Linux based system, which of the following file contains information about dns server i.e nameserver?

/etc/resolve.conf
/etc/hosts
/etc/resolve.conf +
/etc/hostname

### 
On host01, if we have an entry for app01 in /etc/hosts file like 172.168.238.12 app01 
and the DNS server which is used by host01 has 172.168.239.10 as app01's IP then which 
IP host01 will pick for app01 as per priority.

172.168.239.10
172.168.238.12 +

because local recording has highest priority

### On host01, point www.google.com to 127.0.0.1 IP address locally.

#### solution:
```
sudo su -
echo "127.0.0.1 www.google.com" >> /etc/hosts
```
check (there are no nslookup or dig utils on a lab machine)

```
curl -vvv www.google.com
*   Trying 127.0.0.1:80...
```
ok

### On host01, add Google public DNS i.e 8.8.8.8 as a nameserver.

#### solution:
there is no a "systemd-resolved" on this lab "machine" - in a real system with systemd we need to edit /etc/systemd-resolved.conf 
we will edit /etc/resolv.conf

it sill be faster with directly use vi or nano (by me)
```
cat /etc/resolv.conf 
search stratos.xfusioncorp.com
nameserver 127.0.0.11
nameserver 8.8.8.8
options ndots:5
```
ok

### In www.google.com, which is the top level domain?

.com +
www
google

### Which of the following is a sub-domain example?

google
google.com
maps.google.com +
.com

### On host01 we want to resolve name news to news.yahoo.com automatically without 
hard coding its entry in /etc/hosts file. Add the required changes on host01.
#### solution:
add entry to /etc/resolve.conf:
```
search yahoo.com
```

### Which of the following command is used to query a hostname from a DNS server?

ip addr
nslookup +
ifconfig
netstat

