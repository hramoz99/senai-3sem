```
#! / bin / bash
###BEGIN INIT INFO
#Início padrão: 2 3 4 5
###END INIT INFO
```
#### DECLARAÇÃO DA POLÍTICA PADRÃO - RESTRITIVA
```
iptables -P INPUT DROP
iptables -P OUTPUT DROP
iptables -P FORWARD DROP
```
#### LIMPAR AS REGRAS DAS CHAINS DAS TABELAS FILTER E NAT
```
iptables -t filter -F
iptables -t nat -F
```
#### HABILITAR FUNÇÃO ROTEAMENTO
```
echo 1 > / proc / sys / net / ipv4 / ip_forward
```
#### HABILITAR FUNÇÃO DE NAT
```
iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE
```
#### REGRA 0 | ESTADO DO PACOTE | PERMITINDO RETORNO DE TODO PACOTE QUE TEVE SUA IDA LIBERADA
```
iptables -A INPUT -m state --state ESTABELECIDO, RELACIONADO -j ACEITAR
iptables -A SAÍDA -m estado --estado ESTABELECIDO, RELACIONADO -j ACEITAR
iptables -A FORWARD -m state --state ESTABELECIDO, RELACIONADO -j ACEITAR
```
#### LIBERAR O LOCALHOST
##### Baseado em IP - 127.0.0.1
```
iptables -A INPUT -s 127.0.0.1 -j ACEITAR
iptables -A SAÍDA -d 127.0.0.1 -j ACEITAR
```
##### Baseado em Interface - lo
```
iptables -A ENTRADA -i lo -j ACEITAR
iptables -A SAÍDA -o lo -j ACEITAR
```
#### LIBERAR O ACESSO DO CLIENTE 
```
iptables -A INPUT -s 10.10.0.1 -j ACEITAR
iptables -A SAÍDA -d 10.10.0.1 -j ACEITAR
iptables -A FORWARD -s 10.10.0.1 -j ACEITAR
iptables -A FORWARD -d 10.10.0.1 -j ACEITAR
```
#### LIBERAR O ACESSO SSH DO FIREWALL
```
iptables -A INPUT -p tcp --dport 22 -j ACEITAR
iptables -A SAÍDA -p tcp --sport 22 -j ACEITAR

ou

# iptables -A INPUT -sport 22 -p tcp -s 172.31.0.0/24 -j ACEITAR
# iptables -A SAÍDA -sport 22 -p tcp -s 172.31.0.0/24 -j ACEITAR
```
#### REJEITAR "ICMP" DO CLIENTE - GERANDO LOG QUANDO ACIONADO
```
iptables -A FORWARD -s 10.10.0.1 -d 172.31.0.253 -p icmp -j LOG --log-prefix " Tentativa frustrada de LOG "
iptables -A FORWARD -s 10.10.0.1 -d 172.31.0.253 -p icmp -j REJEITAR
```
#### LIBERAR O ICMP PARA TODO CENÁRIO
```
iptables -A INPUT -p icmp -j ACEITAR
iptables -A SAÍDA -p icmp -j ACEITAR
iptables -A FORWARD -p icmp -j ACEITAR
```
#### RESTRINGIR ACESSO SSH 
###### Regra para o cliente
```
iptables -A INPUT -s 10.10.0.1 -p tcp --dport 22 -j ACEITAR
iptables -A SAÍDA -d 10.10.0.1 -p tcp --sport 22 -j ACEITAR
```
##### Regra para servidores
```
iptables -A INPUT -s 172.31.0.0/24 -p tcp --dport 22 -j ACEITAR
iptables -A SAÍDA -d 172.31.0.0/24 -p tcp --sport 22 -j ACEITAR
```
##### Regra para Internet
```
iptables -A ENTRADA -i enp0s3 -p tcp --dport 22 -j ACEITAR
iptables -A SAÍDA -o enp0s3 -p tcp --sport 22 -j ACEITAR
```

#### LIBERAR PROTOCOLO DNS
```
iptables -A FORWARD -p udp --dport 53 -j ACEITAR
iptables -A FORWARD -p udp --sport 53 -j ACEITAR
iptables -A SAÍDA -p udp --dport 53 -j ACEITAR
iptables -A INPUT -p udp --sport 53 -j ACEITAR
```
#### LIBERAR REPOSITÓRIO LINUX
```
iptables -A SAÍDA -d deb.debian.org -j ACEITAR
iptables -A INPUT -s deb.debian.org -j ACEITAR
iptables -A SAÍDA -d security.debian.org -j ACEITAR
iptables -A INPUT -s security.debian.org -j ACEITAR
iptables -A FORWARD -d deb.debian.org -j ACEITAR
iptables -A FORWARD -s deb.debian.org -j ACEITAR
iptables -A FORWARD -d security.debian.org -j ACEITAR
iptables -A FORWARD -s security.debian.org -j ACEITAR
```
#### LIBERAR COMPARTILHAMENTO DE ARQUIVO
```
iptables -A FORWARD -d 172.31.0.252 -p tcp -m multiport --dport 139.445 -j ACEITAR
iptables -A FORWARD -s 172.31.0.252 -p tcp -m multiport --sport 139.445 -j ACEITAR
iptables -A FORWARD -d 172.31.0.252 -p udp -m multiport --dport 137,138 -j ACEITAR
iptables -A FORWARD -s 172.31.0.252 -p udp -m multiport --sport 137,138 -j ACEITAR
```
#### LIBERAR ACESSO A INTERNET (NAVEGAÇÃO)
```
iptables -A FORWARD ! -s 172.31.0.252 -p tcp -m multiport --dport 80.443 -j ACEITAR
# iptables -A FORWARD! -d 172.31.0.252 -p tcp -m multiport --sport 80.443 -j ACEITAR
```
#### LISTAR A CONFIGURAÇÃO ATUAL
```
Clear
iptables -L -nv --line-numbers
```
