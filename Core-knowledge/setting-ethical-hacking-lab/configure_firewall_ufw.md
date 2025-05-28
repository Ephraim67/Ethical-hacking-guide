## Configuring Firewall Rules with UFW

### INTRODUCTION
UFW (uncomplicated firewall) is a firewall configuration tool that runs on top of iptables, included by default within Ubuntu distributions. It provides a streamlined interface for configuring common firewall use cases via the command line.

### Guide to use ufw:

- Check ufw status: ```sudo ufw status```
- Enable ufw: ```sudo ufw enable```
- Disable ufw: ```sudo ufw disable```
- Block an IP address: ```sudo ufw deny from 192.168.X.X```
- Block a subnet: 
