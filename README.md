# dnsmasq
config files and NetSIG DNSMasq presentation documentation
== Note that I'm not using DNSMasq for dhcp.  That's taken care of by my router (for now).
== cool picture to find:
RPiSystem.png
### Tux!

![tux!](https://www.markdownguide.org/assets/images/tux.png) ![Raspberry Pi](RPiSystem.png)
### Installation
install dnsmasq application, and dmsutils so you can see what's going on
```
apt install dnsmasq
apt install dnsutils
```
### Configuration
There are only two files that need to be edited:

one is /etc/dnsmasq.conf and the other is /etc/hosts

cool "grep" command to show config files without comments or empty lines:

```
grep -v "^#" dnsmasq.conf | grep -v "^$"
```

**Note, though, that the dnsmasq.conf file contains lots of good info**

There is a service that runs on the server called dnsmasq and it's controlled by systemd (sorry, everyone ;)

```
systemctl status dnsmasq.servic
```

I found out that dnsmasq will also do cnames.  I haave a wiki, mywiki, that I want to access by the wiki name (mywiki.lpnet.ca) instead of theserver name (wendy.lpnet.ca).

in the /etc/dnsmasq.conf file, I added cname=desired_name,real_name
```
cname = mywiki.lpnet.ca,wendy.lpnet.ca
```

Now I can see where the cname directs to:

```
nslookup mywiki.lpnet.ca
```

Another thing to note:

DNS seems to need some kind of domain name.  There seems to be only one strictly legal unregistered domain name that someone can use for their home network, and that's home.arpa  (RFC 8375) assigned in 2018

There is some indication that .local might still be OK but there are issues with multicast-DNS (?? What is that, anyway??)

.play and .home have been taken.

.example, .invalid, .localhost, and .test are also reserved names, but I didn't like any of them, so I bought lpnet.ca



=======
== Note that I'm not using DNSMasq for dhcp.  That's taken care of by my router (for now).
== cool picture to find:
RPiSystem.png


