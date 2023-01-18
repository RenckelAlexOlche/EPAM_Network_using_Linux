# EPAM_Network_using_Linux



CentOs_Client_2 set up ip 10.92.27.2/24 and Internal Network(Net_3) in VM VirtualBox,
set up ip 172.16.27.2/24 and Internal Network(Net_4) in VM VirtualBox
```
[alex@cnt7 ~]$ cd /etc/sysconfig/network-scripts/

[alex@cnt7 network-scripts]$ ls -al
total 264
drwxr-xr-x. 2 root root  4096 Dec 12 22:57 .
drwxr-xr-x. 6 root root  4096 Dec  6 18:06 ..
-rw-r--r--. 1 root root   310 Dec 12 23:09 ifcfg-enp0s3
-rw-r--r--. 1 root root   348 Dec 13 00:23 ifcfg-enp0s8
-rw-r--r--. 1 root root   254 May 22  2020 ifcfg-lo


[alex@cnt7 network-scripts]$ sudo nano ifcfg-enp0s3
IPADDR=10.92.27.2
PREFIX=24

[alex@cnt7 network-scripts]$ sudo nano ifcfg-enp0s8
IPADDR=172.16.27.2
PREFIX=24

[alex@cnt7 network-scripts]$ sudo nmcli connection reload

[alex@cnt7 network-scripts]$ nmcli con sh
NAME    UUID                                  TYPE      DEVICE 
enp0s3  c472028f-2e97-4402-b1ae-8287d3e592a3  ethernet  enp0s3 
enp0s8  1f586766-b2ef-3030-b857-eda8dbf32301  ethernet  enp0s8 
virbr0  822397f2-dcd4-4128-a58f-89fa151a93bb  bridge    virbr0 

[alex@cnt7 network-scripts]$ reboot (sometimes changes not work)

[alex@cnt7 network-scripts]$ ping 10.92.27.1
PING 10.92.27.1 (10.92.27.1) 56(84) bytes of data.
64 bytes from 10.92.27.1: icmp_seq=1 ttl=64 time=0.561 ms
64 bytes from 10.92.27.1: icmp_seq=2 ttl=64 time=0.345 ms
64 bytes from 10.92.27.1: icmp_seq=3 ttl=64 time=0.354 ms
^C
--- 10.92.27.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2001ms
rtt min/avg/max/mdev = 0.345/0.420/0.561/0.099 ms

[alex@cnt7 network-scripts]$ ping 172.16.27.1
PING 172.16.27.1 (172.16.27.1) 56(84) bytes of data.
64 bytes from 172.16.27.1: icmp_seq=1 ttl=64 time=0.348 ms
64 bytes from 172.16.27.1: icmp_seq=2 ttl=64 time=0.339 ms
^C
--- 172.16.27.1 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1005ms
rtt min/avg/max/mdev = 0.339/0.343/0.348/0.019 ms
```
Download on each os in VM VirtualBox :~ sudo apt-get install openssh-server
```
[alex@cnt7 network-scripts]$  ssh renckel@10.92.27.1
The authenticity of host '10.92.27.1 (10.92.27.1)' can't be established.
ECDSA key fingerprint is SHA256:ourONnAEawFtsDUQo6D4Hh4LhDNCDvWdQ3N1dxApoEU.
ECDSA key fingerprint is MD5:5d:17:18:35:51:75:2d:1a:44:25:b9:62:70:e5:93:38.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '10.92.27.1' (ECDSA) to the list of known hosts.
renckel@10.92.27.1's password: 
Welcome to Ubuntu 22.04.1 LTS (GNU/Linux 5.15.0-56-generic x86_64)
 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage
  System information as of Mon Dec 12 10:52:22 PM UTC 2022
  System load:  0.0               Users logged in:         1
  Usage of /:   29.6% of 9.75GB   IPv4 address for enp0s3: 10.0.2.15
  Memory usage: 5%                IPv4 address for enp0s8: 10.7.92.1
  Swap usage:   0%                IPv4 address for enp0s9: 10.92.27.1
  Processes:    103
3 updates can be applied immediately.
To see these additional updates run: apt list --upgradable
Failed to connect to https://changelogs.ubuntu.com/meta-release-lts. Check 
your Internet connection or proxy settings
Last login: Mon Dec 12 20:33:10 2022
renckel@server1:~$ 

renckel@server1:~$ exit
logout
Connection to 10.92.27.1 closed.

[alex@cnt7 network-scripts]$  ssh oleksii@172.16.27.1
The authenticity of host '172.16.27.1 (172.16.27.1)' can't be established.
ECDSA key fingerprint is SHA256:1JbPly/G4McsmIlcAlbC89QAohqMdIcKO+GmXDfIwhg.
ECDSA key fingerprint is MD5:2b:ba:ef:4d:fb:72:0a:a3:bd:d3:92:4a:ca:d7:ed:23.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '172.16.27.1' (ECDSA) to the list of known hosts.
oleksii@172.16.27.1's password: 
Welcome to Ubuntu 22.04.1 LTS (GNU/Linux 5.15.0-56-generic x86_64)
 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage
  System information as of Tue Dec 13 12:55:14 AM EET 2022
  System load:  0.10986328125      Processes:               197
  Usage of /:   53.8% of 19.02GB   Users logged in:         1
  Memory usage: 22%                IPv4 address for enp0s3: 10.7.92.2
  Swap usage:   0%                 IPv4 address for enp0s8: 172.16.27.1
 * Strictly confined Kubernetes makes edge and IoT secure. Learn how MicroK8s
   just raised the bar for easy, resilient and secure K8s cluster deployment.
   https://ubuntu.com/engage/secure-kubernetes-at-the-edge
0 updates can be applied immediately.
Last login: Thu Dec  8 18:48:39 2022 from 192.168.1.9
oleksii@oleksii-VirtualBox:~$ 
```


Ubuntu22_Server_1 set up ip 10.0.2.15/24 and NAT in VM VirtualBox,
set up ip 10.92.27.1/24 and Internal Network(Net_2) in VM VirtualBox, 
set up ip 10.7.92.1/24 and Internal Network(Net_3) in VM VirtualBox
```
renckel@server1:~$ cd /etc/netplan/

renckel@server1:~$ sudo nano *.yaml
network:
  version:2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: yes
    enp0s8:
      addresses: [10.7.92.1/24]
    enp0s9:
      addresses: [10.92.27.1/24]

renckel@server1:~$ sudo netplan apply

renckel@server1:~$ ping 10.7.92.2
PING 10.7.92.2 (10.7.92.2) 56(84) bytes of data.
64 bytes from 10.7.92.2: icmp_seq=1 ttl=64 time=0.289 ms
64 bytes from 10.7.92.2: icmp_seq=2 ttl=64 time=0.295 ms
^C
--- 10.7.92.2 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1018ms
rtt min/avg/max/mdev = 0.289/0.292/0.295/0.003 ms

renckel@server1:~$ ping 10.92.27.2
PING 10.92.27.2 (10.92.27.2) 56(84) bytes of data.
64 bytes from 10.92.27.2: icmp_seq=1 ttl=64 time=0.278 ms
64 bytes from 10.92.27.2: icmp_seq=2 ttl=64 time=0.336 ms
^C
--- 10.92.27.2 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1021ms
rtt min/avg/max/mdev = 0.278/0.307/0.336/0.029 ms

renckel@server1:~$ ssh oleksii@10.7.92.2
The authenticity of host '10.7.92.2 (10.7.92.2)' can't be established.
ED25519 key fingerprint is SHA256:EyF1r1gi1LnV8wtDjJ+rxNd4lslgKNk28ukklKpqiYw.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.7.92.2' (ED25519) to the list of known hosts.
oleksii@10.7.92.2's password: 
Welcome to Ubuntu 22.04.1 LTS (GNU/Linux 5.15.0-56-generic x86_64)
 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage
  System information as of Tue Dec 13 06:06:55 PM EET 2022
  System load:  0.0                Processes:               208
  Usage of /:   53.8% of 19.02GB   Users logged in:         1
  Memory usage: 29%                IPv4 address for enp0s3: 10.7.92.2
  Swap usage:   0%                 IPv4 address for enp0s8: 172.16.27.1
0 updates can be applied immediately.
Failed to connect to https://changelogs.ubuntu.com/meta-release-lts. Check 
your Internet connection or proxy settings
Last login: Tue Dec 13 00:55:15 2022 from 172.16.27.2
oleksii@oleksii-VirtualBox:~$ 
```


Ubuntu22_Client_1set up ip 10.7.92.2/24 and Internal Network(Net_2) in VM VirtualBox, 
set up ip 172.16.27.1/24 and Internal Network(Net_4) in VM VirtualBox
```
oleksii@oleksii-VirtualBox:~$ cd /etc/netplan/

oleksii@oleksii-VirtualBox:/etc/netplan$ ls -al
total 20
drwxr-xr-x   2 root root  4096 гру 13 00:36 .
drwxr-xr-x 140 root root 12288 гру  8 17:56 ..
-rw-r--r--   1 root root   233 гру 13 00:20 01-network-manager-all.yaml

oleksii@oleksii-VirtualBox:/etc/netplan$ sudo nano *.yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: no
      addresses: [10.7.92.2/24]
    enp0s8:
      dhcp4: no
      addresses: [172.16.27.1/24]

oleksii@oleksii-VirtualBox:/etc/netplan$ sudo netplan apply

oleksii@oleksii-VirtualBox:/etc/netplan$ ping 172.16.27.2
PING 172.16.27.2 (172.16.27.2) 56(84) bytes of data.
64 bytes from 172.16.27.2: icmp_seq=1 ttl=64 time=0.367 ms
64 bytes from 172.16.27.2: icmp_seq=2 ttl=64 time=0.379 ms
^C
--- 172.16.27.2 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1010ms
rtt min/avg/max/mdev = 0.367/0.373/0.379/0.006 ms

oleksii@oleksii-VirtualBox:/etc/netplan$ ping 10.7.92.2
PING 10.7.92.2 (10.7.92.2) 56(84) bytes of data.
64 bytes from 10.7.92.2: icmp_seq=1 ttl=64 time=0.026 ms
64 bytes from 10.7.92.2: icmp_seq=2 ttl=64 time=0.035 ms
^C
--- 10.7.92.2 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1015ms
rtt min/avg/max/mdev = 0.026/0.030/0.035/0.004 ms

oleksii@oleksii-VirtualBox:~$ ssh alex@172.16.27.2
The authenticity of host '172.16.27.2 (172.16.27.2)' can't be established.
ED25519 key fingerprint is SHA256:dOyuy0mdsjzXWTdSvt0OtRErjU81JaNGp0kWa1WQLzQ.
This host key is known by the following other names/addresses:
    ~/.ssh/known_hosts:1: [hashed name]
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '172.16.27.2' (ED25519) to the list of known hosts.
alex@172.16.27.2's password: 
Last login: Tue Dec 13 00:29:12 2022
[alex@cnt7 ~]$ exit

oleksii@oleksii-VirtualBox:~$ ssh renckel@10.7.92.1
The authenticity of host '10.7.92.1 (10.7.92.1)' can't be established.
ED25519 key fingerprint is SHA256:UnmkxAl5TT0pb+MnM+quHpOE56MfSwO4DD+lwGVXalI.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.7.92.1' (ED25519) to the list of known hosts.
renckel@10.7.92.1's password: 
Welcome to Ubuntu 22.04.1 LTS (GNU/Linux 5.15.0-56-generic x86_64)
 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage
  System information as of Mon Dec 12 11:22:50 PM UTC 2022
  System load:  0.0               Users logged in:         1
  Usage of /:   29.6% of 9.75GB   IPv4 address for enp0s3: 10.0.2.15
  Memory usage: 5%                IPv4 address for enp0s8: 10.7.92.1
  Swap usage:   0%                IPv4 address for enp0s9: 10.92.27.1
  Processes:    103
3 updates can be applied immediately.
To see these additional updates run: apt list --upgradable
Failed to connect to https://changelogs.ubuntu.com/meta-release-lts. Check
your Internet connection or proxy settings
Last login: Mon Dec 12 22:52:22 2022 from 10.92.27.2
renckel@server1:~$ 
```
