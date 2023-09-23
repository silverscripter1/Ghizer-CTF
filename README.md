# NerdHerd CTF
A step by step walk through for the NerdHerd CTF on Tryhackme
---

### Link: https://tryhackme.com/room/nerdherd

---

## Step 1: Enumeration

Lets begin with nmap, a popular enumeration tool!

*more here: https://www.kali.org/tools/nmap/ Nmap scans a machine to discover live services that are running, these services are sometimes vulnerable*

Command: nmap `<machine_ip> -sV -sC -p- ` (We use -sV to determine the service version of the services running on the open ports and we use -p- to scan all ports, because by default nmap only scans 1000 ports, we can change it to scan all 65,000 using -p-)

Anways! Lets look at our results

![image](https://github.com/silverscripter1/Ghizer-CTF/assets/92340426/e624d659-0754-4faf-b673-45fda9e3b59d)]

We see there are 5 ports open, port 21, 22, 139, 445 and 1337

To explain the 5 ports;

Port 21: 21 is used for transferring files, FTP stands for file transfer protocol and is a very good way to gather information (as a malicious attacker )if the port has bad security configurations

A really common security misconfiguration on port 21 involves allowing anyone to connect and log on with the username "anonymous" and provide no password. This can allow people to freely access potentially sensitive
information.

Port 22: This is an SSH service and is probably the most secure port in this CTF, you can only access the SSH service with the correct username and password. Its very secure because it allows remote access to the machine running the service

Port 139 and 445: This is samba, or SMB for short. It is a common file sharing service and is basically a more secure FTP service and with more features, so knowing how to enumerate these ports is very important

Port 1337: This is running http, this stands for Hyper Text Transfer Protocol and is the website port, if a port is running http, it can be accessed via web browser. I'd also like the mention http is most commonly on port 80 and is super uncommon to find on other ports.

--- 

For simplicity I'll start with the lowest port and move up

# Port 21

![image](https://github.com/silverscripter1/Ghizer-CTF/assets/92340426/54ae54f1-f4c1-44ff-937b-c1c7743482dd)

We can access the FTP port with `FTP <machine_ip>`. Off the bat it queries us for a username. Revealed in the nmap scan it tells us anonymous login is allowed, using this and providing no username by just hitting the enter key when asked for one. We can see what files are here, we can use `ls -lah` and there is a directory named "pub"

![image](https://github.com/silverscripter1/Ghizer-CTF/assets/92340426/75656f6b-3c1e-4bf7-bba0-24b8fed86dd0)

We change to pub and there is 2 files, an image and a secret directory called ".jokesonyou" We can download these to our machine using `mget *`
