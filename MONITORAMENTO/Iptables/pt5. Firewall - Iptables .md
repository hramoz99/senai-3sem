# AUTOMAÇÃO ./firewall.sh" - Roteamento e Firewall

    1) Copiar as últimas duas linhas do arquivo '/root/firewall.sh'

    2) Cole em /etc/init.d/firewall) 
    
    3) Limpar as regras das tabelas filter e nat
         iptables -t nat -F -> apaga as informações da tabela filter

--------------------------------------------------------------------

### `DESAFÍO`

    4) Restringir SSH do SRVFW-BERLIM para cliente, servidores e internet

    5) Liberar protocolo DNS

    6) Liberar repositório (LINUX) vigente

## SCRIPT - SOLUÇÃO

* Restringir SSH para cliente, servidores e internet

#### RESTRINGIR SSH PARA CLIENTE, SERVIDORES E INTERNET | REGRA PARA CLIENTE
        iptables -A INPUT -s 10.10.0.1 -p tcp --dport 22 -j ACEITAR
        iptables -A SAÍDA -d 10.10.0.1 -p tcp --sport 22 -j ACEITAR

#### REGRA PARA SERVIDORES
        iptables -A INPUT -s 172.31.0.0/24 -p tcp --dport 22 -j ACEITAR
        iptables -A SAÍDA -d 172.31.0.0/24 -p tcp --sport 22 -j ACEITAR

#### REGRA PARA INTERNET
        iptables -A ENTRADA -i enp0s3 -p tcp --dport 22 -j ACEITAR
        iptables -A ENTRADA -o enp0s3 -p tcp --sport 22 -j ACEITAR


#### LIBERAR PROTOCOLO DNS
        iptables -A FORWARD -p udp --dport 53 -j ACEITAR
        iptables -A FORWARD -p udp --sport 53 -j ACEITAR
        iptables -A SAÍDA -p udp --dport 53 -j ACEITAR
        iptables -A INPUT -p udp --sport 53 -j ACEITAR

        
#### LIBERAR REPOSITORIO LINUX
        iptables -A SAÍDA -d deb.debian.org -j ACEITAR
        iptables -A INPUT -s deb.debian.org -j ACEITAR
        iptables -A SAÍDA -d security.debian.org -j ACEITAR
        iptables -A SAÍDA -s security.debian.org -j ACEITAR
        iptables -A FORWARD -d deb.debian.org -j ACEITAR
        iptables -A FORWARD -s deb.debian.org -j ACEITAR
        iptables -A FORWARD -d security.debian.org -j ACEITAR
        iptables -A FORWARD -s security.debian.org -j ACEITAR

        
