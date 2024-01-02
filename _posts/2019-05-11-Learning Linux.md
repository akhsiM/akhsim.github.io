---
title: Linux Journey
layout: post-toc
tags: linux software
---

<img class="mx-auto w-1/2" src="{{site.baseurl}}/assets/img/orgNotesImages/FS-Hierarchy.png">

## Process Utilization
### top
*1st line:* /(uptime)/ Current time | How long the system been running | How many logged-on users | System load avg.
*2nd line:* Tasks that are running, sleeping, stopped and zombied.
*3rd line*: CPU Information - us = user CPU time that aren't niced | sy = system CPU time (kernel & kernel processes) | ni = %CPU running niced processes | id = CPU idle time | wa = CPU wait time (waiting for I/O) | hi = hardware interrupts, %CPU serving hardware interrupts | si = software interrupts | st = steal time (virtual machine)
*4th and 5th lines* are for Memory and Swap Usage

### lsof
/list open files/

List of open files and the associated processes that is using the file(s).

`lsof <filename>`
`lsof <directory>`

### fuser
/file user/

This shows information about the process that is using file or "the file user".
Use `fuser -v`.

Example of lsof and fuser below:

```bash

kkennynguyen@Kennys-ThinkPad-X1C:`/pCloudDrive/Documents/OrgNotes/MeetingNotes$ lsof .
lsof: WARNING: can't stat() tracefs file system /sys/kernel/debug/tracing
      Output information may be incomplete.
COMMAND   PID         USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
bash     6574 kkennynguyen  cwd    DIR   0,56     4096   45 .
lsof    14492 kkennynguyen  cwd    DIR   0,56     4096   45 .
lsof    14493 kkennynguyen  cwd    DIR   0,56     4096   45 .

kkennynguyen@Kennys-ThinkPad-X1C:`/pCloudDrive/Documents/OrgNotes/MeetingNotes$ fuser -v .
                     USER        PID ACCESS COMMAND
/home/kkennynguyen/pCloudDrive/Documents/OrgNotes/MeetingNotes:
                     kkennynguyen   6574 ..c.. bash

```

### Process threads

Threads are very similar to *Processes* in that they are both used to execute programs. They are often referred to as =lightweight= processes. If a process has one thread it would be called a single threaded process (versus multithreaded process). All processes have _at least one thread_. 

Processes, however, operate with their own isolated system resources, whereas *threads can share resources amongst each other easily*. Therefore it is more efficient to have multi-threaded application than a multi-process application.

To see threads use `ps m` which shows PID and their respective threads underneath, denoted by a `--`.

### uptime

Used for *CPU monitoring*. This shows similar stdout to first line of *top*

*Load Average* represents the average number of CPU load in 1, 5, 15 minutes intervals. CPU load is the average number of processes waiting to be processed by CPU. E.g: 100% CPU = CPU Load of 1, 200% = 2..etc..

When observing CPU Load, we *have to* account the number of CPU cores, e.g if we have a load average of 1, and we have a quad-core processor, the CPU Load is only just affecting 25% of the CPU. We should think of each core as a single lane on a freeway that is the processor. 

We can view the amount of cores by `cat /proc/cpuinfo` or `inxi`.

### iostat (I/O monitong)

Used for monitoring CPU usage as well as *disk usage*. 
/N/A on default but can be installed by `sudo apt install sysstat`./

- First part is CPU information:

|---------------------------------------------------------------------------|--------------------------------------------------------------------------------|---------------------------------------------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|
| %user                                                                     | %nice                                                                          | %system                                                 | %iowait                                                                                | %steal                                                                                                               | %idle                                                                             |
| %CPU Utilization that occurer while executing at user level (application) | %CPU Utilization that occured while executing at user level with nice priority | %CPU Utilization that occured at system level (kernel). | % Time that CPU were idle during which the system had an outstanding disk I/O request. | % Time spent in involuntary wait by virtual CPU or CPUs while the hypervisor was servicing another virtual processor | % Time that CPU were idle and that the system did *not* have an outstanding request |

- Second part is Disk Utilization:

|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------|---------------------------------------------------------|-------------------------|----------------------------|
| tps                                                                                                                                                                                             | kB_read/s                                           | kB_wrtn/s                                               | kB_read                 | kB_writn                   |
| No. of Transfer per Second. A transfer is an I/O request to the device. Multiple logical requests can be combined into a single I/O request to the deivce. A transfer is of indeterminate size. | Amount of Data read from device (kilobytes per sec) | Amount of Data written to the device (kilobyte per sec) | Total number of kB read | Total number of kB written |
 
### vmstat

Used for monitoring memory usage.

The Fields are as follow:

- *procs*
  + Number of processes for run time
  + Number of processes in uninterruptible sleep
- *memory*
  + swpd: Amount of virtual memory used
  + free: Amount of free memory
  + buff: Amount of memory used as buffers
  + cache: Amount of memory used as cache
- *io*
  + bi: Amount of blocks in (received from block device)
  + bo: ................out... sent out......
- *system*
  + in: Number of interrupts per sec
  + cs: Number of context switches per sec
- *cpu* - similar to 2nd line of *top* 
  + us: Time spent in user time
  + sy: Time spent in kernel time
  + id: Time spent idle
  + wa: Time spent waiting for IO
    
### sar (Continuous Monitoring)

`sudo apt install sysstat` is needed.
Then, modify the ENABLE field in /etc/default/sysstat

Once set-up, sysstat will automatically collect data. Logs are stored in /var/log/sysstat/saXX where XX is the day

Then you can do:

`sudo sar -q`: List details from start of the day
`sudo sar -r`: list details of memory usage from start of day
`sudo sar -P`: list details of CPU usage

or `sar -q /var/log/sysstat/sa02`

### cron jobs (Job scheduler)

Time-based job scheduler in Unix-like computer OS. Suitable for scheduling *repetitive tasks*.

*Format*:
=MM(0-59) HH(0-23) DD(1-31) MM(1-12) DD(0-7) /path/to/script=

*Example*:
`30 08 /home/kkennynguyen/scripts/test`
Run "test" every day at 08.30am.

*How-to*:
To create a cron job, just edit the crontab file by `crontab -e`. Cron is driven by a crontab file.

## System Logging

### syslog - General
   
In order to allow us to have a human-readable journal of all events that are happening on the system, data about what the system/kernel/daemons, etc on our system is doing is always saved in the form of logs. This data is kept in the /var directory.

=*Logs are kept in /var, which stands for variables*=

This is done by a service called *syslogs* that sends the information as messages to the system logger.

Syslogs contain many components, one being an important daemon running called syslogd (or rsyslogd) that waits for event message, do some filtering and send to a file or do nothing.

Syslog isn't the only thing that manage logs. Many applicaations write their own logging rules and generate different log files in differnt directories. 

Generally the format of logs should include a timestamp and event details.

### syslog - How to

#+Name: See Logs about UniWireless from last 650 lines of syslog file
```bash
kkennynguyen:log> tail -n 650 syslog | grep UniWireless
May  2 15:01:33 Kennys-ThinkPad-X1C wpa_supplicant[870]: wlp4s0: Trying to associate with f8:4f:57:84:91:ff (SSID='UniWireless' freq=5805 MHz)
May  2 15:11:38 Kennys-ThinkPad-X1C wpa_supplicant[870]: wlp4s0: SME: Trying to authenticate with b0:aa:77:d7:b2:cf (SSID='UniWireless' freq=5220 MHz)
May  2 15:11:39 Kennys-ThinkPad-X1C wpa_supplicant[870]: wlp4s0: Trying to associate with b0:aa:77:d7:b2:cf (SSID='UniWireless' freq=5220 MHz)

```

Right now syslog is running:

```bash 
  PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND                
  862 syslog    20   0  263036   5144   3528 S   0.0  0.1   0:01.89 rsyslogd     

```


*syslog* service manages and reports to the *System Logger*. To find out what files are maintained by the System Logger, inspect the config files in /etc/rsyslogd. In this file, rules are denoted on the left colum and actions are denoted on the right column. =Not every application uses rsyslogd=.

To manually send a log, use `logger`.
```bash

kkennynguyen:OrgNotes> logger hello
kkennynguyen:OrgNotes> logger hello 2
kkennynguyen:OrgNotes> logger hello
kkennynguyen:OrgNotes> tail -n 3 /var/log/syslog
May  3 06:58:49 Kennys-ThinkPad-X1C kkennynguyen: message repeated 3 times: [ hello]
May  3 06:58:53 Kennys-ThinkPad-X1C kkennynguyen: hello 2
May  3 06:58:55 Kennys-ThinkPad-X1C kkennynguyen: hello


```

### Kernel logging

legacy: /var/log/dmesg

present:

logs are stored in /var/log/kern.log
dmesg is nicer

*Example*:
```bash

kkennynguyen:log> dmesg | tail -n 3
[30244.736014] IPv6: ADDRCONF(NETDEV_CHANGE): wlp4s0: link becomes ready
[30244.787220] wlp4s0: Limiting TX power to 30 (30 - 0) dBm as advertised by be:e3:3f:6d:fa:61
[31651.952554] perf: interrupt took too long (4018 > 3988), lowering kernel.perf_event_max_sample_rate to 49750

kkennynguyen:log> tail -n 3 kern.log
May  3 06:37:05 Kennys-ThinkPad-X1C kernel: [30244.736014] IPv6: ADDRCONF(NETDEV_CHANGE): wlp4s0: link becomes ready
May  3 06:37:06 Kennys-ThinkPad-X1C kernel: [30244.787220] wlp4s0: Limiting TX power to 30 (30 - 0) dBm as advertised by be:e3:3f:6d:fa:61
May  3 07:00:33 Kennys-ThinkPad-X1C kernel: [31651.952554] perf: interrupt took too long (4018 > 3988), lowering kernel.perf_event_max_sample_rate to 49750

```

### Authentication logging

stored in */var/log/auth.log*. Contains system authorization logs, such as user login and authentication method used.

*Sample snippet* 
```bash

May  3 06:47:49 Kennys-ThinkPad-X1C sudo: kkennynguyen : TTY=pts/0 ; PWD=/home/kkennynguyen/pCloudDrive/Documents/OrgNotes ; USER=root ; COMMAND=/usr/local/bin/apt install trash-cli

```
### Log files management

Answer: *logrotate*
- Does log management
- Has a config file that allows specifying how many and what logs to keep, etc.
- ran out of *cron* once a day.
Location: `/etc/logrotate.d`

## Network sharing

### File Sharing

#### scp
/secure copy/

Works exactly the same way cp works but allows copy from hosts on same network.

Use these formats:
- *Copy a file from localhost to remote host*: `$ scp path/to/file username@remotehost.com:/path/to/directory`
- *Copy a file from remote host to localhost*: `$scp username@remotehost.com:/path/to/file /local/directory`
- *For directory, use* `$scp -r`

#### rsync
remote synchronization

Similar to scp but rsync uses an algorithm that *checks data and only copy the differences*.
This makes rsync ideal for file transfer flexibility and *directory synchronization* remotely, locally, data backups, large data transfer, etc.

Format: `$ rsync -[options] /src/dir /dest/dir`
- options:
  + v - verbose
  + r - recursive (must use for directories)
  + z - compressed for easier transfer
  + h - human readable


### #HTTP Server#

Python has a *SimpleHTTPServer* module. It sets up a Simple HTTP with std Get and Head request handlers. The HTTP server can be accessed via =http://IPADDRESS:8000=

Default port: =8000=

Format: `$python -m SimpleHTTPServer`
The *-m* is to run a module as a script.

### NFS
/Network File System/

NFS is a service that allows a server to share directories and files with one or more clients over network.

Setting up:
`$ sudo service nfsclient start`

### Samba
/Server Message Block/

SMB is a protocol that was created to share files between Linux and Windows OS (Mac also has SMB).

Later it was cleaned up and optimized in the form of Common Internet File Share *(CIFS)* protocol.

samba needs to be installed `$ sudo apt install samba`
Configuration file for sambe is at `/etc/samba/smb.conf`. The default conf file comes with a lot of commented out code. Good place to start.

- set up a user for samba `$ sudo smbpasswd -a [username]` 
- accesing a samba share on Linux `$ smbclient /path/to/directory -u [username]`
- mount a samba share: `$ sudo mount -t cifs servername:/directory /mount/point -o -u user=domain\username`
## Network Basics
### Common components

| Common Components | Definition                                                |
|-------------------|-----------------------------------------------------------|
| ISP               | Internet Service Provider                                 |
| Router            | Mostly wireless, allows local devices to talk to Internet |
| WAN               | Wide Area Network, network that encompasses *everything*    |
| WLAN              | Network between router and any wireless device            |
| LAN               | Network between router and any wired device               |
| Hosts             | Each machine on network is known as as a host             |

### OSI Model

*Theoretical* model of networking
This model shows how a packet traverses through a network in *seven* different layers. 
Gave birth to TCP/IP model.

### #TCP/IP Model#

This model is what the Internet is based off of.
*Actual/ Practical* of networking

The TCP/IP model uses [[TCP/IP Protocol suite][TCP/IP Protocol suite]].

#### #Packets:#
#<<<Packet>>> 

- Packets are used to transmit data across networks.
- Consists of a *header* and *payload*.
- Header contains 'sent from' and 'to' info. Headers is appended as a packet moves across networks.

#### Ports
<<port>> 
IP Addresses aren't specific enough to send data to a certain process or service. 
So they have to use a communication channel via *Ports*. 

```
HTTP Service uses Port 80. 
So webpage data is sent over Port 80.
```

#### Network Addressing
/Packets need information where they are going to./

- *MAC Address:* Unique Identifer as a *hardware* address | Never changes | Given when network card was manufactured | Denoted with OUI from manufacturer
- *IP Address:* Used to identify a devic eover network | hardware dependent | *Software* | Changes with Network
- *Hostnames:* Hostnames take the IP address and mask it with a human readable name, e.g instead of 192.124.243.123, myhost.com

### TCP/IP Protocol suite

#### Application Layer
#<<<Application layer>>>
  + Presents data in a user-friendly format.
  + Top layer of TCP/IP model
  + Determines how computer program (e.g web browser) interfaces with the transport layer services
  + It uses: 
    - HTTP - Hypertext Transfer Protocol: used for webpages
    - SMTP - Simle Mail Transfer Protocol: used for email transmission
  + Communicates with Transport Layer through a specified Port, e.g SMTP uses Port 25.

Data: User-friendly format 
#### Transport Layer
#<<<Transport Layer>>>

  + Determine how data will be transmitted i.e checking ports, data integrity and delivery of packets
  + Helps transfer data in a way that networks can read it. It breaks data up into chunks (=segments=) that will be transported and put back together.
  + It includes *two* protocols:
    - *TCP* - Transmission Control Protocol: 
      - Reliable | Actually check if data is received or not.
      - Uses port and *Three-way handshake* to establish connection between client and server.
	1. Host A send `SYNchronize` packet to Host B.
	2. Host B receives Host A's SYN.
	3. Host B sends a `SYNchronize-ACKnowledgement`.
	4. Host A receceives SYN-ACK.
	5. Host A sends ACK.
	6. Host B receives ACK.
	7. TCP Socket connection is now `Established`.
      - Once TCP connection is established, data is sent over in different segments and are tracked with TCP sequence number for re-assembling purpose.
    - *UDP* - User Data Protocol:
      - Unreliable | Does not care if data is received or not.
      - Good option for application where speed is more important than 100% data delivery. E.g: Media Streaming.
  + Transport Layer sends segments to Network Layer. 

Data: broken up into segments
#### Network Layer
#<<<Network Layer>>>

  + Receives the segment from Transport Layer then encapsulate it into an IP packet, adding these to the Packet Header:
    * The IP address of source host (Sent-From)
    * The IP address of destination host (Sent-To)
  + Specifies how to move packets between hosts and across networks, from source to destination.
  + For the Internet, it is made up of many smaller networks which are called *subnets*. All subnets on the Internet are connected together in some way. IP addresses define the rules to travel to different subnets.
  + It uses:
    - IP - Internet Protocol: Help route packets from one machine to another
    - ICMP - Internet Control Message: Helps tell us what is going on, such as error messages and debugging information.
  + With the packet containing info about Sent-From and Sent-To, it is sent to the physical layer.

Data: Segments are encapsulated into IP Packets.
#### Link Layer
#<<<Link layer>>>
 
 + Bottom of the TCP/IP model | is hardware specific.
  + Specifies how to send data across a physical piece of hardware i.e data travelling physically through ethernet, fibre, etc.
  + Packet is encapsulated once more into a *frame*. The frame header attaches the source and destination MAC addresses of hosts, checksums and packet separators so that receiver can tell when a packet end.
  + Link layer first attaches source MAC address to the frame header, then to find destination's MAC address, it uses *Address Resolution Protocol* (#<<<ARP>>>)
    * ARP is used within the *same* network.
    * If Dest is not on the same network, the packet would then be sent to the next router until it's on the same network.
    * On the same network, systems would then use the ARP look-up table which stores info about what IP addresses are associated with what MAC address. If the value is not on the look-up table, the system would then send a *broadcast* message to to all hosts, asking which host has the destination IP Address. The machine with the requested IP address will then reply with an ARP packet containing the IP address, as well as its MAC address.

Data: Packet is encapsulated into frame. 
#### Example of a Packet Traversal down TCP/IP layer

1. A sends B an email: This data originates from the Application Layer then get sent to the Transport Layer.
2. The Transport Layer then encapsulates the data into TCP (or UDP) header to form a segment, which also contains information about source and destination's TCP (or UDP) Port. The segment is then sent to Network Layer.
3. The Network Layer encapsulates the TCP segment inside an IP packet, as well as adding header information about source and destination's IP Address. This packet is then routed to the Link Layer.
4. The packet then reaches A's physical hardware and gets encapsulated in a frame. The source and destination MAC gets added to the frame.
5. B receives this data frame through physical layer, checks each frame for data integrity, then de-encapsulates the frame contents and sends the IP packet to the Network layer.
6. The network layer then reads the packet to find source and destination IP that was attached in 3.. It checks if its IP address is the same as destination IP address, which it is. It de-encapsulates the packet and send the segment to the transport layer.
7. The transport layer de-enscapsulates the segments, check TCP (or UDP) port numbers, that was attached in step 2., then makes a connection with the application layer based on the Port number.
8. The application layer receives data from transport layer on the specified port and presents it to B in the form of human readdable format.

### DHCP Overview
/Dynamic Host Configuration Protocol/

- Assigns IP addresses, subnet masks and gateway to machines.
  E.g Similarly to how a phone carrier assigns a number to our Cell Phone.
- However IP addresses are *leased* for a certain amount of time, depending on the lease settings.
- Prevents from IP addresses duplicacy.
- In a regular home settings, router acts as DHCP server.

#### How it works

1) *DHCP DISCOVER* message is broadcasted to search for a DHCP server by the client.
2) *DHCP OFFER* is replied by DHCP server after it receives the broadcast message. The offer contains a packet with DHCP lease time, subnet mask, IP address, etc.
3) *DHCP REQUEST* is broadcasted by the client one more time to let all DHCP servers know which offer was accepted.
4) *DHCP ACK* is sent by the server as acknowledgement.

## Subnetting 

### IPv4

*IPv4* is a unique address. An IPv4 address actually consists of *two* parts. 
- *Network Portion*: tells which network the host is on
- *Host Portion*: tells which host on the network it is 

An IPv4 address is seperated into four *octets* by periods. Each octet = 8 bits = 1 byte. So an IPv4 Address = 4 bytes.

In the below example, IP address = 172.20.10.10
```
$ ifconfig
wlp4s0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.20.10.10  netmask 255.255.255.240  broadcast 172.20.10.15
        inet6 fe80::2d0d:a03d:ce5:49f4  prefixlen 64  scopeid 0x20<link>
        ether 00:28:f8:26:35:c7  txqueuelen 1000  (Ethernet)
        RX packets 3134004  bytes 3746812190 (3.7 GB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 1011961  bytes 167469589 (167.4 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### Subnet
*Subnet definition*: Group of hosts with IP Addresses that are similar in a certain way. Usually these hosts are in proximate location to each other and it's easier to send data between. This is similar to properties having the same *Postcode*.

```
123.45.67.8 and 123.45.67.9 are on the same subnet. The common numbers are network prefix.
```

### Subnet Masks

*Subnet masks determine what part of IP Address is the network portion and what part is the host portion.*
Typically it looks like `255.255.255.0`.

The 255 portion is the *mask*. 

/Explanation: Each octet has 1 byte, or 8 bits. Each bit is denoted by a 0 or 1 in binary form. When binary numbers are used, 1 means *ON* and 0 means *OFF*. '11111111' means 255./

Subnets are commonly denoted by the network prefix followed by the subnet mask e.g `123.234.0.0/ 255.255.0.0`.

*Why?* Subnetting is used to segment networks and control the traffic within network. Host on one subnet can't interact with hosts on another subnet. To connect to a public address, we need to connect subnets together. 
E.g If my host 192.168.1.129 is connected to a local network of 192.168.1.129/25, it can reach to any host on that network. However to reach hosts on the rest of the Internet, it needs to communicate through the *router*. Traditionally on most networks with a subnet of `255.255.255.0`, the router is at address 1 of the subnet which is `192.168.1.1` 

### Subnet Math
#<<<Subnet Math>>> can be used to figure *how many hosts* we can have on one subnet./

Let's say we have an IP Address of 192.168.1.0 and a subnet mask of 255.255.255.0, let's line up these numbers in binary form:

`192.168.1.0    = 11000000.10101000.00000001.00000001`
`255.255.255.0  = 11111111.11111111.11111111.00000000` 

The IP Address is masked by the subnet mask. When we see a *1*, it is masked and we pretend we don't see it.
Therefore, the only possible hosts are from the 00000000 region. 

Total number: 256
Minus one for host number (192.168.1.0): 255
Minus one for broadcast address (192.268.1.255): 254 

*Conclusion*: We have 254 addresses ranging with IP address from 192.168.1.1 to 192.168.1.254
 
### CIDR
/Classless inter-domain routing/

Used to represent a subnet mask in a more compact way.
CIDR notation of `10.42.3.0/24` is similar to `10.42.3.0/255.255.255.0`. It includes both the subnet prefix and the subnet mask.
CIDR indicates the amount of _bits_ used as the network prefix, i.e 24 bits means three octets (out of total four).

*Example*: 123.12.24.0/23 means that the first 23 bits are used for subnet mask. 
In this case, 9 bits (32 - 23) are used to represent host.
I.e number of usable hosts = 2^9 - 2 = 510 (Subnet Math)
### NAT
/Network address translation/

The Internet cannot see our IP Address. 
NAT makes a device like our router act as an intermediary between our private network and the Internet. The router represents the entire network of hosts on the Internet. Think of it like a Service Desk of the whole office.

i.e when we connect to Google, our router is the intermediary between us and Google.com. Google doesn't know about us, all they can see is the router.
### IPv6

IPv6 protocol was created to allow more hosts to the Internet as there is a *finite* number of available IP Addresses. However adoption for IPv6 is rather slow. It is not meant to replace IPv4 as they are rather meant to complement each other. 
## Routing
### Router
<<router>>

#### Definition
A router enables machine on a network to communicate with each other as well as with other networks/ Internet. On a typical router there is a LAN port that allows machines to be connected to the same Local Area Network and there will also be a *Internet uplink port* that connects the network to the Internet. This is sometimes labelled *WAN* (Wider Area Network). 

All network activities go through the router. The router decides where our network packets go and which one comes in. It routes our packets between multiple networks to get from its source host to destination host.

#### How

Router works similarly to a *local* mail deliverer. It knows exactly where the packet (letter) has to go without handing it to a different router (post office). 

### Hops
<<hops>> 
<<hop>>
As packets move across networks they travel in hops. A hop is how we roughly measure the distance that the packet must travel from src to dest.

E.g from Host A to Host B, there are two hops. Each hop is an intermediate device like the router that we must pass through.

### Packet SWITCHING/ ROUTING & FLOODING

Packet Switching is basically receiving, processing and forwarding data to the destination device.

Packet Routing is a process of creating routing table so we can Switching later.

Before routing, flooding was used. If a router doesn't which way to send a packet then every incoming packet is sent through every outgoing link except the one it arrived on.

### Routing Table

```
kkennynguyen:OrgNotes> route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
default         192-168-1-1.tpg 0.0.0.0         UG    600    0        0 wlp4s0
link-local      0.0.0.0         255.255.0.0     U     1000   0        0 wlp4s0
192.168.1.0     0.0.0.0         255.255.255.0   U     600    0        0 wlp4s0

```

#### Destination
In the first field, we have a destination IP address of 192.168.1.0 i.e *any packet* that tries to go to this network, goes out through Wifi card (wlp4s0).

0.0.0.0s means unspecified addresses or unknown. i.e if I want to send a packet to a random public IP address, the routing table doesn't know where that goes so it denotes it as 0.0.0.0 and routes the packet to the *gateway*.
#### Gateway
<<gateway>>
If we are sending packet that isn't on the same network, it will be sent to this gateway address.
Gateway is aptly named after being a *Gateway to another network*.
#### Genmask
This is the subnet mask. It is used to figure out what IP addresses match what destination.
#### Flags
    *UG* - Network is up and is a Gateway
    *U* - Network is up 
#### Iface
This is the intereface that our packet will be going out of, eth0 means Ethernet whereas wlp4s0 means Wireless device.

### Path of a packet

#### Local

1) First the local host will compare the dest IP to see if it's in the same subnet by looking at the subnet mask.
2) When packets are sent they need to have a src MAC address, destination MAC address, src IP and dest IP, at this point we do not know the dest MAC yet.
3) To get the dest host, we use ARP to broadcast a request on the local network to find out the MAC address.
4) Now the packet can be sent.

#### Outside of Network

1) First the local machine will compare the dest IP address, since it's outside of network it does not see the MAC address of dest host.
2) So our packet now looks at the routing table. It doesn't know the address of the dest IP, so it sends it out to the default gateway (another router). At this point the packet contains src IP, dest IP and src MAC (no dest MAC). So it also sends out an ARP request to get the MAC address of the default [[gateway][*gateway*]].
3) The router looks at the packet and confirm dest MAC. However it's not the final dest IP address so it keeps looking at the routing table to forward th epacket to another IP address that can help the packet move along to its destination. *Everytime the packet moves, it strips the old src and dest MAC address and updates the packet with new src and dest MAC address*.
4) Once the packet gets forwarded to the same network, ARP is used to find the final destination MAC.
5) During this process, src and dest IP on packet header remain unchanged.
## Network Config

### Network interfaces

A network interface is how the kernel links up the software side of networking to the hardware.

#### ifconfig

The `ifconfig` command shows the interface name on the left side and detailed information on the right side. Common interfaces are eth0, wlan0, lo (loopback). The loopback interface is used to represent your computer as it loops you back to yourself. This is good for debugging or connecting to servers running locally. 

```sh
kkennynguyen:OrgNotes> ifconfig
enp0s31f6: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        ether c8:5b:76:da:5e:4c  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
        device interrupt 16  memory 0xec300000-ec320000  

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 167913  bytes 17460711 (17.4 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 167913  bytes 17460711 (17.4 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

wlp4s0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.151  netmask 255.255.255.0  broadcast 192.168.1.255
        inet6 fe80::228:f8ff:fe26:35c7  prefixlen 64  scopeid 0x20<link>
        ether 00:28:f8:26:35:c7  txqueuelen 1000  (Ethernet)
        RX packets 3731110  bytes 4201734573 (4.2 GB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 1422285  bytes 260356720 (260.3 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

```

The status of interfaces can be UP or DOWN. Thus `ifup` brings interface up and `ifdown` brings interface down.

#### ip 

The `ip` command allows us to manipulate the networking stack of a system. Depending on the distro you are using it may be the preferred method of manipulating netwokr.

`ip link show` shows interface information for all interfaces.
`ip -s link show eth0` shows the statistics of an interfaces.
`ip address show` shows all IP addresses allocated to interfaces.
`ip link set wlp4s0 up` brings interface wlp4s0 up.
`ip link set wlp4s0 down` brings interface wlp4s0 down.

You can also add an IP address to an interface by `ip address add 192.168.1.1/24` dev eth0.
### route

Add a new route: `$ sudo route add -net 192.168.2.1/23 gw 10.11.12.1`
Delete a route : `$ sudo route del -net 192.168.2.1/23`

### dhclient

dhclient starts up on boot and gets a list of network interfaces from the dhclient.conf file. 

`$ sudo dhclient -r` ends the current DHCP lease
`$ sudo dhclient wlp4s0` starts a new DHCP lease on interface wlp4s0.

### Network Manager

Network Manager is a daemon to configure networks automatically. 
It's a GUI applet but we can also interact with it using CLI tools.

`nmcli` allows utilisation of Network Manager via CLI instead of GUI. It is usefule for servers, headless machines and terminal.

```
wlp4s0: connected to TheWerriBeans-5G
        "Intel Wireless 8265 / 8275 (Dual Band Wireless-AC 8265)"
        wifi (iwlwifi), 00:28:F8:26:35:C7, hw, mtu 1500
        ip4 default
        inet4 192.168.1.151/24
        route4 192.168.1.0/24
        route4 0.0.0.0/0
        route4 192.168.1.0/24
        inet6 fe80::228:f8ff:fe26:35c7/64
        route6 ff00::/8
        route6 fe80::/64

enp0s31f6: unavailable
        "Intel Ethernet Connection (4) I219-V (ThinkPad X1 Carbon 5th Gen)"
        ethernet (e1000e), C8:5B:76:DA:5E:4C, hw, mtu 1500

lo: unmanaged
        "lo"
        loopback (unknown), 00:00:00:00:00:00, sw, mtu 65536

DNS configuration:
        servers: 192.168.1.1
        interface: wlp4s0
```
### ARP

`$ arp` checks the locally stored ARP cache on system.
## DNS

IP address is the low-level IP networking way of identifying a host. 

DNS allows a high-level, human readdable method of keeping track of websites and hosts by name instead of IP addresses. 

It's like a *contact list* for the Internet.

DNS is fundamentally a *distributed database* of hostnames to IP addresses. 

### Process

#### Local DNS Server

After go browse to https://helloworld.com/ with DNS, essentially we funnel our way down until we reach the DNS server that knows of that domain.

First place our host ask is our *local DNS server* however it doesn't know and starts asking the Root Servers via recursive DNS server provided by ISP.

#### Root Servers

There are 13 Root Servers on the Internet, they are mirrored and distributed around the world to handle DNS request for the Internet. So really there are hundreds of servers that are working. They control information about Top-Level Domain like .com, .net, .org.

The Root server doesn't know where helloworld.com is, so it tells us to ask .com Top-Level Domain DNS server. 

#### Top-Level Domain

So now we send another request to the name server that knows about '.com. addresses. The TLD doesn't have it in their zone file but it sees a record for the name server for helloworld.com. Then it gives us the IP address of that name server and tells us to look there.

#### Authoritative DNS Server

Now we send the final request to the DNS Server that actually has the record we want. The name server sees that it has a zone file for helloworld.com and there is a resource record for www for this host. It then gives us the IP address of this host. Finally we can see https://www.helloworld.com/
### /etc/hosts

`/etc/hosts` file contains mapping of some hostnames to IP addresses. 
It typically contains localhost address listed as default.

Fun example:
`$ sudo nano /etc/hosts` 
add 123.45.6.7 www.google.com to the file

We can't go to Google anymore because our hosts first look locally for IP address mapping, it never actually reaches DNS to find Google.com. 
## Network Troubleshooting

### ICMP 
The *Internet Control Message Protocol* (ICMP) is part of the TCP/IP protocol suite. it is used to send updates and error messages for debugging network issues.

Each ICMP message contains a type, code and checksum field. 

The Type field is the type of ICMP message, the code is sub-type and describe more information about the message and the checksum is to detect any issues with the integrity of the message.

For example, ICMP Type 3 = Destination Unreachable | Code 0 = Network Unreachable; Code 1 = Host Unreachable.
### ping

This is the simplest networking tool.
It works by sending ICMP Type 8 request - *echo request* to the destination host and waits for an ICMP reply (Type 0). 

```ping google.com
PING google.com (172.217.25.142) 56(84) bytes of data.
64 bytes from syd15s03-in-f14.1e100.net (172.217.25.142): icmp_seq=1 ttl=56 time=12.8 ms
64 bytes from syd15s03-in-f14.1e100.net (172.217.25.142): icmp_seq=2 ttl=56 time=14.8 ms
64 bytes from syd15s03-in-f14.1e100.net (172.217.25.142): icmp_seq=3 ttl=56 time=14.7 ms

--- google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2002ms
rtt min/avg/max/mdev = 12.833/14.158/14.873/0.937 ms

```

=icmp_seq= denotes the sequence number of packet sent.
If we do a *ping* and see missing sequence number, that indicates connectivity issue and not all packets are getting through. If sequence number is out of wack, connection is probly very slow.

=ttl= denotes Time-To-Live, used as a *hop counter*. Each time the packet make a hop, ttl is decremented by one. TTL gives packet a lifespan.

=time= denotes roundtrip time, from sending the echo request to getting an echo reply.
### traceroute

To see how packets are getting routed. 
It works by sending packets with increasing TTL value, starting with one until it finally reaches the destination IP address with receive an ICMP Echo Reply message.

```traceroute google.com
traceroute to google.com (172.217.25.142), 30 hops max, 60 byte packets
 1  192-168-1-1.tpgi.com.au (192.168.1.1)  2.451 ms  2.438 ms  4.106 ms
 2  nme-sot-dry-bras21-Lo20.tpgi.com.au (10.20.22.137)  7.627 ms  8.556 ms  10.843 ms
 3  203-219-155-2.tpgi.com.au (203.219.155.2)  18.241 ms  18.570 ms  18.552 ms
 4  syd-apt-ros-crt2-be-10.tpgi.com.au (202.7.171.153)  20.730 ms  21.547 ms  21.537 ms
 5  203.29.134-125.tpgi.com.au (203.29.134.125)  22.426 ms  22.426 ms  22.410 ms
 6  209.85.149.84 (209.85.149.84)  23.937 ms  24.812 ms  24.740 ms
 7  108.170.247.49 (108.170.247.49)  22.882 ms  18.220 ms  19.163 ms
 8  74.125.37.155 (74.125.37.155)  17.113 ms 74.125.37.201 (74.125.37.201)  14.458 ms  15.368 ms
 9  syd15s03-in-f14.1e100.net (172.217.25.142)  14.562 ms  13.445 ms  14.316 ms

```

The above indicates 9 messages with TTL values from 1 to 9 were sent until the last one with TTL=9 reaches google.com.

Each line represents a hop, i.e a router or machine that is between myself and target. 

Last three columns represent the round-trip time of a packet to get to that router. By default we send 3 along the route.

`$ ping google.com` retunrs similar round-trip time to last message with TTL=9.

### #Well Known Ports#

We can get a list of well-known ports by looking at `/etc/services`:

```
kkennynguyen:OrgNotes> cat /etc/services | grep 'http\|https\|smtp'
smtp		25/tcp		mail
http		80/tcp		www		# WorldWideWeb HTTP
https		443/tcp				# http protocol over TLS/SSL
urd		465/tcp		ssmtp smtps  # URL Rendesvous Directory for SSM
http-alt	8080/tcp	webcache	# WWW caching service
http-alt	8080/udp

```

*Format*: service      port number/transport layer
### netstat

#### socket
First, what is a *socket*? 

A socket is an *interface* that allows program to send and receive data while a Port is used to identify which application should send or receive data. 

The socket address is the combination of IP address and port.
Every connection between a host and destination requires a *unique socket*. 

E.g: HTTP is a service that runs on Port 80, however we can have many HTTP connections at once. Each individual connection is maintained by one socket.

#### netstat
```
kkennynguyen:OrgNotes> netstat -at
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State      
tcp        0      0 0.0.0.0:37319           0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:netbios-ssn     0.0.0.0:*               LISTEN     
tcp        0      0 localhost:5939          0.0.0.0:*               LISTEN     
tcp        0      0 localhost:domain        0.0.0.0:*               LISTEN     
tcp        0      0 localhost:ipp           0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:microsoft-ds    0.0.0.0:*               LISTEN     
tcp        0      0 192-168-1-151.tpg:55994 ec2-54-200-147-0.:https ESTABLISHED
tcp        0      0 192-168-1-151.tpg:45480 edge-star-shv-01-:https ESTABLISHED
tcp        0      0 192-168-1-151.tpg:41488 binapi10.pcloud.c:https ESTABLISHED
tcp        0      0 192-168-1-151.tpg:57146 203-219-43-209.tp:https ESTABLISHED
tcp        0      0 192-168-1-151.tpg:55908 40.100.148.2:https      ESTABLISHED
tcp        0      0 192-168-1-151.tpg:45520 edge-star-shv-01-:https ESTABLISHED
tcp        0      0 192-168-1-151.tpg:46802 edge-star-mini-sh:https ESTABLISHED
tcp        0      0 192-168-1-151.tpg:45518 edge-star-shv-01-:https ESTABLISHED
tcp        0      0 192-168-1-151.tpg:45238 edge-star-shv-01-:https ESTABLISHED
tcp        0      0 192-168-1-151.tpg:52436 40.100.151.114:https    ESTABLISHED
tcp        0      0 192-168-1-151.tpg:42456 binapi15.pcloud.c:https ESTABLISHED
tcp6       0      0 [::]:netbios-ssn        [::]:*                  LISTEN     
tcp6       0      0 ip6-localhost:ipp       [::]:*                  LISTEN     
tcp6       0      0 [::]:microsoft-ds       [::]:*                  LISTEN   
```

netstat -a command shows all, listening and non-listening sockets included. 
-t flag shows ONLY tcp connections.

Columns definition (L-R):
- Proto: Protocol, TCP or UDP
- Recv-Q: data that is queued to be received
- Send-Q: data that is queued to be sent
- Local Address: Locally connectd host
- Foreign Address: Remotely connected host
- State: State of *socket*. There are a few, i.e LISTENING, SYN_SENT, ESTABLISHED, CLOSED_WAIT..etc..
### Basic of Packet Analysis

There are two extremely popular packet analyzer - Wireshark and tcpdump.
They allow low-level analysis of networking by scanning our network interfaces and capture the activity before outputing the information for us to see.

Between the two, Wireshark is more powerful although tcpdump is simpler.

`$ sudo tcpdump -i wlp4s0` captures packet data on an interface.

```
kkennynguyen:OrgNotes> sudo tcpdump -i wlp4s0 | grep google
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on wlp4s0, link-type EN10MB (Ethernet), capture size 262144 bytes
07:27:19.226424 IP Kennys-ThinkPad-X1C.47957 > _gateway.domain: 52045+ [1au] A? apis.google.com. (44)
07:27:19.226775 IP Kennys-ThinkPad-X1C.45589 > _gateway.domain: 42540+ [1au] A? plus.l.google.com. (46)

```

*Understanding the Output*

- The first field is a timestamp of the network activity. Format: hh:mm:ss and fractions of seconds till midnight. It follows the kernet's clock.
- *IP* - This contains the protocol information.
- Next is the *source* and *destination* address. =Kennys-ThinkPad-X1C > _gateway.domain=.

You can also do `$ sudo tcpdump -w /some/file` to write output to a file for logging informatio/

