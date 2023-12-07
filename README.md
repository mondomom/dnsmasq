# this documentation is available on:  

# https://www.github.com/mondomom/dnsmasq.git

# dnsmasq ![Raspberry Pi](images/raspitr.png)
config files and NetSIG DNSMasq presentation documentation

***Note that I'm not using DNSMasq for dhcp.  That's taken care of by my router (for now)***

### Installation
install dnsmasq application, and dnsutils so you can see what's going on
```
sudo apt install dnsmasq
sudo apt install dnsutils
```
### Server Configuration
There are only two files that need to be edited:

one is /etc/dnsmasq.conf and the other is /etc/hosts

cool "grep" command to show config files without comments or empty lines:

```
grep -v "^#" dnsmasq.conf | grep -v "^$"
```
Here's dnsmasq.conf:
```
lynn@fedora:~/MyCode/dnsmasq$ grep -v "^#" dnsmasq.conf | grep -v "^$"
server=8.8.8.8
local=/lpnet.ca/
domain=lpnet.ca
cache-size=1500
cname=mywiki.lpnet.ca,wendy.lpnet.ca
dhcp-mac=set:client_is_a_pi,B8:27:EB:*:*:*
dhcp-reply-delay=tag:client_is_a_pi,2
```

**Note, though, that the dnsmasq.conf file contains lots of good info**

Here's /etc/hosts:
```
127.0.0.1       localhost
::1             localhost ip6-localhost ip6-loopback
ff02::1         ip6-allnodes
ff02::2         ip6-allrouters


# real hardware
10.0.0.2                sammy sammy.lpnet.ca
10.0.0.5                accumulus accumulus.lpnet.ca
10.0.0.7                wynn wynn.lpnet.ca
10.0.0.8                wynn11 wynn11.lpnet.ca
10.0.0.9                hyperbox hyperbox.lpnet.ca

# VMs
10.0.0.26               wendy wendy.lpnet.ca
10.0.0.28               harvey harvey.lpnet.ca

# Raspberry Pi's
10.0.0.30               blueberry blueberry.lpnet.ca
10.0.0.32               cherry cherry.lpnet.ca
10.0.0.35               raspberrypi raspberrypi.lpnet.ca
10.0.0.36               cranberry cranberry.lpnet.ca
10.0.0.37               blackberry blackberry.lpnet.ca

# Kubernetes Stuff
10.0.0.81               katy1 katy1.lpnet.ca

```
There is a service that runs on the server called dnsmasq and it's controlled by systemd (sorry, everyone ;)

```
systemctl status dnsmasq.service
```

I found out that dnsmasq will also do cnames.  I have a wiki, mywiki, that I want to access by the wiki name (mywiki.lpnet.ca) instead of theserver name (wendy.lpnet.ca).

in the /etc/dnsmasq.conf file, I added cname=desired_name,real_name
```
cname = mywiki.lpnet.ca,wendy.lpnet.ca
```

Now I can see where the cname directs to:

```
nslookup mywiki.lpnet.ca
```


=== Host Configuration
  * each host in my network (the way it is so far) needs to have the DNS IP address added to it.
  * I've found that it's easier to do this on each host once, than forever looking up addresses, but YMMV
  * 

Another thing to note:

DNS seems to need some kind of domain name.  There seems to be only one strictly legal unregistered domain name that someone can use for their home network, and that's home.arpa  (RFC 8375) assigned in 2018

There is some indication that .local might still be OK but there are issues with multicast-DNS (?? What is that, anyway??)

.play and .home have been taken

.example, .invalid, .localhost, and .test are also reserved names, but I didn't like any of them, so I bought lpnet.ca



=======  
== Note that I'm not using DNSMasq for dhcp.  That's taken care of by my router (for now).  
== cool picture to find:  
RPiSystem.png


