# dnsmasq
config files and NetSIG DNSMasq presentation documentation
== Note that I'm not using DNSMasq for dhcp.  That's taken care of by my router (for now).
== cool picture to find:
RPiSystem.png

=== Installation
install dnsmasq application, and dmsutils so you can see what's going on
```
apt install dnsmasq
apt install dnsutils
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
I found out that dnsmasq will also do cnames.  I haave a wiki, mywiki, that I want to access by the wiki name (mywiki.lpnet.ca) instead of theserver name (wendy.lpnet.ca).

in the /etc/dnsmasq.conf file, I added cname=desired_name,real_name
```
cname = mywiki.lpnet.ca,wendy.lpnet.ca
```

Now I can see where the cname directs to:

```
nslookup mywiki.lpnet.ca

=======
== Note that I'm not using DNSMasq for dhcp.  That's taken care of by my router (for now).
== cool picture to find:
RPiSystem.png


