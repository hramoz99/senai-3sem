SCRIPT - CISCO ASA

    1) Acesso para todos - www do DMZ
    2) Somente outside pode pingar o DMZ
    3) Somente inside pode acessar o ftp do DMZ

#---------------------------------------

en
conf t

! Regra1
access-list role extended permit tcp host 192.168.10.2 host 192.168.20.2 eq www
access-group role in interface outside
access-list role extended permit tcp host 192.168.20.2 eq www host 192.168.1.2
access-group role in interface DMZ

! Regra2
access-list role extend permit icmp host 192.168.10.2 host 192.168.20.2

! Regra3
access-list role extended permit tcp host 192.168.20.2 eq ftp host 192.168.1.2
