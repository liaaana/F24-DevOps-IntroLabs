# Operating Systems & Networking Lab
Exploring operating systems and networking fundamentals in a DevOps context. 

## Task 1: Operating System Analysis
Analyzed and understood key aspects of the operating system's performance and uptime.
1. **Analyzed system boot time**:

Command: `systemd-analyze`


Output:
```
Startup finished in 3.260s (kernel) + 13.064s (userspace) = 16.324s 
graphical.target reached after 12.768s in userspace
```


Command: `systemd-analyze blame`

Slow servises (>1s):
```
2min 42.277s apt-daily.service
2min 34.492s apt-daily-upgrade.service
      6.883s apparmor.service
      2.559s fstrim.service
      2.346s snapd.seeded.service
      2.337s snapd.apparmor.service
      2.287s snapd.service
      1.972s systemd-networkd-wait-online.service
      1.906s dev-mapper-ubuntu\x2d\x2dvg\x2dubuntu\x2d\x2dlv.device
      1.806s cloud-init-local.service
      1.301s dev-loop2.device
      1.299s dev-loop3.device
      1.293s dev-loop5.device
      1.286s dev-loop8.device
      1.196s dev-loop1.device
      1.187s dev-loop4.device
      1.179s dev-loop7.device
      1.076s dev-loop6.device
      1.076s dev-loop0.device
```

2. **Checked system load and uptime**:

Command: `uptime`

Output:
```
 19:52:31 up 16:07,  1 user,  load average: 0.04, 0.07, 0.06
```

Command: `w`

Output:
```
19:52:44 up 16:07,  1 user,  load average: 0.11, 0.08, 0.07
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
ubuntu   tty2     tty2             Tue08   35:17m  0.02s  0.01s /usr/libexec/gn
```
3. **Observations regarding system boot time, load, and uptime**:

- The system boot process completed in **16.324 seconds**, **most of the delay was caused by userspace** (13.064 seconds). 
- The system has been up for over **16 hours** with a low load average of 0.04, 0.07, and 0.06 over the last 1, 5, and 15 minutes, respectively. 
- The system has **one active user** session and CPU usage is low.


## Task 2: Networking Analysis

Performed network diagnostics and analyzed DNS resolution to understand network paths and latency.

Faced errors and fixed them by
```
sudo apt update
sudo apt install traceroute
sudo apt update
sudo apt install dnsutils
```

1. **Traceroute**:

Command: `traceroute innopolis.university`

Output:
```
traceroute to innopolis.university (213.159.212.4), 30 hops max, 60 byte packets
 1  * * _gateway (192.168.64.1)  0.294 ms
 2  10.8.30.1 (10.8.30.1)  78.271 ms  78.216 ms  78.164 ms
 3  37.120.133.97 (37.120.133.97)  101.867 ms  102.938 ms  102.877 ms
 4  146.70.4.102 (146.70.4.102)  90.539 ms  90.494 ms  90.170 ms
 5  146.70.4.123 (146.70.4.123)  86.097 ms * 146.70.4.125 (146.70.4.125)  85.958 ms
 6  hundredgige0-0-2-3.bb2n.lon2.uk.m247.ro (146.70.1.127)  92.323 ms hundredgige0-0-1-3.bb1n.ams2.nl.m247.ro (89.44.212.117)  90.957 ms hundredgige0-0-0-25.bb1n.ams2.nl.m247.ro (146.70.1.228)  99.562 ms
 7  hundredgige0-0-1-0.core1.ams1.nl.m247.ro (77.243.185.138)  99.514 ms hundredgige0-0-0-25.bb1n.ams2.nl.m247.ro (146.70.1.228)  111.811 ms hundredgige0-0-2-1.core1.ams1.nl.m247.ro (146.70.1.123)  111.662 ms
 8  vlan2907.as09.zur1.ch.m247.com (212.103.51.77)  214.601 ms  214.563 ms  220.017 ms
 9  ae18-xcr1.skt.cw.net (195.2.8.205)  235.964 ms vlan2907.as09.zur1.ch.m247.com (212.103.51.77)  219.828 ms *
10  ae18-xcr1.skt.cw.net (195.2.8.205)  235.694 ms  235.647 ms  235.628 ms
11  91.108.51.16 (91.108.51.16)  161.652 ms  163.723 ms  136.422 ms
12  mail-ru.gw.gblnet.ru (109.239.134.30)  128.804 ms 91.108.51.16 (91.108.51.16)  138.304 ms  126.810 ms
13  * * *
14  ext01.university.innopolis.ru (213.159.212.4)  124.841 ms !X  121.883 ms !X  126.577 ms !X

```
2. **Used `dig` to perform a DNS lookup for a specified domain name**:

Command: `dig innopolis.university`

Output:
```
; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> innopolis.university
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 46711
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;innopolis.university.		IN	A

;; ANSWER SECTION:
innopolis.university.	891	IN	A	213.159.212.4

;; Query time: 3 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Wed Sep 18 19:59:08 UTC 2024
;; MSG SIZE  rcvd: 65

```

3. **Observations regarding the network path, latency, and DNS resolution**:

- The `traceroute` to `innopolis.university` (IP: 213.159.212.4) revealed a total of 14 hops, with latency increasing notably around the 6th to 9th hops.
- The `dig` command successfully resolved the domain `innopolis.university` to its IP address **213.159.212.4** with a query time of **3 milliseconds**, indicating low latency and efficient DNS resolution.
