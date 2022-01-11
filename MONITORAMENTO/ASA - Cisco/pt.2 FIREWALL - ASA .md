FIREWALL - ASA (CISCO) - 14/09


    Segurança 0 ---> Segurança 100 = acesso negado
    Segurança 100 <--- Segurança 0 = acesso permitido

    Acess-lists (ACLs) são criadas para que o tráfego flua entre segurança mais baixa para a segurança mais alta

    Origem (source) - segurança mais baixa --> segurança mais alta (destination)

    Em uma interface podemos ter apenas UMA entrada (inside) e UMA saída (outside)

    Em uma mesma ACL podemos ter inúmeras regras desde que sejam aplicadas em interfaces diferentes
-------------------------------------

SECURITY-LEVEL 

 outside = 0 (INTERNET)
 DMZ = 50 (DMZ)
 inside = 100 (LOCAL/LAN)

ACL

* Permitir tráfego da internet para DMZ (www)
    PC0 <---> Server0

    Teste com http://192.168.20.2 (na WEB do PC0)

* Permitir ping DMZ para LOCAL/LAN
    PC1 <---> Server0
    192.168.1.2 <---> 192.168.20.2

-------------------------------------

SCRIPT ASA - CISCO
en
conf t

# Interface g1/1 - outside
int g1/1
nameif outside
ip add 192.168.10.1
no sh

# Interface g1/2 - DMZ
int g1/2
nameif DMZ
ip add 192.168.20.1
security-level 50
no sh

# Interface g1/3 - inside
int g1/3
nameif inside
ip add 192.168.1.1
no sh

# ACL - ex1
exit
access-list ex1 extend permit tcp host 192.168.10.2 host 192.168.20.2 eq www
access-group ex1 in interface outside

# ACL - ex2
access-list ex2 extend permit icmp host 192.168.20.2 host 192.168.1.2
access-group ex2 in interface DMZ

ou 

! Utilizar a mesma regra (Em uma mesma ACL podemos ter inúmeras regras, desde que sejam aplicadas em interfaces diferentes)

# ACL - ex1
access-list ex1 extend permit icmp host 192.168.20.2 host 192.168.1.2
access-group ex1 in interface DMZ

