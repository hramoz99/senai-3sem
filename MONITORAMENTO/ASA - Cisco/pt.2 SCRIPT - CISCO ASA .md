        SCRIPT - CISCO ASA

en
conf t
int g1/1
nameif outside
int g1/2
nameif dmz
security-level 50
ip add 192.168.20.1
no sh
int g1/3
nameif inside
ip add 192.168.1.1
no sh
exit
access-list T1 extend permit icmp any any
access-group T1 in interface outside
access-group T1 in interface dmz
access-group T1 in interface inside
int management 1/1
nameif gerencia
ip add 172.16.0.1
no sh
exit
username admin password Senai@132
ssh 172.16.0.0 255.255.0.0 gerencia
aaa authentication ssh console LOCAL
ssh timeout 60
write memory
