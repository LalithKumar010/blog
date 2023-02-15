---
title: "How Hackers use DNS Spoofing to redirect victims to fake websites"
date: 2022-08-09T18:50:40+05:30
thumbnail: /Images/DNSSpoof.png
draft: false

---
# Introduction
____________________________________________________________________

Welcome Guys, 
In this blog we are going to see **How hackers use basic DNS Spoofing to redirect victims to fake websites**

This blog is divided into 2 parts:

1) Theory behind DNS Spoofing
2) Practical Scenario
	1) Preparing the weapons to perform the attack
	3) Performing the attack


# Theory behind DNS Spoofing
___________________________________________________

Lets understand 2 terms first:
1) DNS
2) Spoofing

## What is DNS ?
**DNS** stands for **D**omain **N**ame **S**ystem
Every webserver you see in the world has an IP address (like 157.240.16.35). Since this is difficult for humans to remember and verify the correct website. People thought to make domain name which can help them in remembering the name of the site. 

In a simple way. You use contacts application in your phone to store necessary contact numbers under their name. In the same way, websites use DNS to store their IP addresses under their name.

### How can this help ?

- It can help people to detect fake websites (owned by bad guys) which look like the real website because they can easily remember the domain name
- It can help people to remember the website name so that they always dont need to remember the site name 



##  What is Spoofing ?
**Spoofing** is the act of disguising a communication from an unknown source as being from a known, trusted source.

*In simple terms,* Spoofing attack enables us to impersonate (act) as a object which is trusted by the target. 

**Example:** Acting like a wifi router and listening to all data which is sent by the phone to the router. This is known as ARP Spoofing (this topic comes in the next part).

So here when we combine these both terms we can clearly understand the meaning


**DNS Spoofing** is an attack by the attacker who makes the victim computer believe that it is a DNS Server which has correct set of DNS records (records of IP address and their Domain Names). 

So here the attacker will use this attack to provide fake IP address with the some other Domain Name which makes the users  think this is the correct domain.

![](/Images/DNSSpoofing.png)

# Practical Scenario
 So now comes the interesting part. **How do we perform attack ?**
 
For this we need Linux based operating system running as a virtual machine or host operating system (preferabbly Kali Linux or Parrot Security)

## Preparing  the necessary weapons

**Bettercap:**
This tool helps us to automate the process of DNS Spoofing

**Kali Linux / Parrot Security**
```bash
sudo apt-get update -y
sudo apt install bettercap -y
```

**Ubuntu / Other Debian based Linux Operating Systems**

```bash
sudo apt-get update -y
sudo apt install golang git build-essential libpcap-dev libusb-1.0-0-dev libnetfilter-queue-dev -y
go get -u github.com/bettercap/bettercap
```


# Performing The Attack
## Before performing the attack:
- Make sure that you and target are connected to same network (same WIFI, LAN)
- Get the IP address of  the target
- Know the name of the interface
```bash
sudo apt install net-tools -y
ifconfig -a
```
![](/Images/ifconfig.png)
OR
```bash
ip a
```
![](/Images/ipa.png)
Check the IP subnet and choose the device

To know the IP address of the target you can use
- FING (Android application allows  to detect the phones and devices connected to same network) **This works very fast**
- netdiscover (Linux package which helps to get the IPs of the machines) **This takes time**
```bash
sudo apt install netdiscover -y
sudo netdiscover -i <interface_name>  -r <ip_range> # generally in wifis the range is 192.168.0.1/24
```
![](/Images/netdiscover.png)
This scan  will take time make sure to wait atleast for 5 min
- You can use NMAP but it has less detection rates as it uses ICMP packets which most of the windows machines reject them 
- ![](/Images/nmap.png)

As we know all the details lets start performing attack. Here im using my virtual interface on virtual machine

**Usage:**
```bash
sudo bettercap -iface <interface_name> 

```

# Battleground Setup
So here in the ~~battleground~~ Lab, I have setup 2 machines the client and the attacker machine.
- Windows (Victim/Client)
- Parrot Security (Bad guy/ Attacker)

For the Video version of it. Please use the link below

<iframe width="560" height="315" src="https://www.youtube.com/embed/cFHySTVRkkI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
<div id="disqus_thread"></div>
<script>
    /**
    *  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
    *  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables    */
    /*
    var disqus_config = function () {
    this.page.url = PAGE_URL;  // Replace PAGE_URL with your page's canonical URL variable
    this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
    };
    */
    (function() { // DON'T EDIT BELOW THIS LINE
    var d = document, s = d.createElement('script');
    s.src = 'https://lalithkumar010-com.disqus.com/embed.js';
    s.setAttribute('data-timestamp', +new Date());
    (d.head || d.body).appendChild(s);
    })();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>

