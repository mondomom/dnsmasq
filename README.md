# dnsmasq
config files and NetSIG DNSMasq presentation documentation
== Note that I'm not using DNSMasq for dhcp.  That's taken care of by my router (for now).
== cool picture to find:
RPiSystem.png

=== Installation
```
apt install dnsmasq
```
=== Configuration
There are only two files that need to be edited:

one is /etc/dnsmasq.conf and the other is /etc/hosts

cool "grep" command to show config files without comments or empty lines:

```
grep -v "^#" dnsmasq.conf | grep -v "^$"
```

There is a service that runs on the server called dnsmasq and it's controlled by systemd (sorry, everyone ;)

```
systemctl status dnsmasq.service

```.
=======
== Note that I'm not using DNSMasq for dhcp.  That's taken care of by my router (for now).
== cool picture to find:
RPiSystem.png


>>>>>>> 9a73b0157c6d29a89c05b6a4febe31fc90e783f5
