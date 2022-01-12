# REMOÇÃO DE LINHAS NÃO UTILIZADAS 

 #### LINHAS "APAGADAS"

    #iptables -A SAÍDA -o lo -j ACEITAR
    #iptables -A FORWARD -p tcp -m multiport --sport 139.445 -j ACEITAR
    #iptables -A FORWARD -p tcp -m multiport --sport 137,138 -j ACEITAR
    #iptables -A FORWARD! -d 172.31.0.252 -p tcp -m multiport --dport 80.443 -j ACEITAR
    #iptables -A SAÍDA -d 10.10.0.1 -p tcp --sport 22 -j ACEITAR
    #iptables -A SAÍDA -d 172.31.0.0/24 -p tcp --sport 22 -j ACEITAR
    #iptables -A FORWARD -o enpos3 -p tcp --sport 22 -j ACEITAR
    #iptables -A FORWARD -p udp --sport 53 -j ACEITAR
    #iptables -A INPUT -p udp --sport 53 -j ACEITAR
    #iptables -A INPUT -s deb.debian.org -j ACEITAR
    #iptables -A INPUT -s security.debian.org -j ACEITAR
    #iptables -A FORWARD -s deb.debian.org -j ACEITAR
    #iptables -A FORWARD -s security.debian.org -j ACEITAR

__________________________________________________________________________________________ 

## SCRIPT - "BACKUP STATELESS"

    #! / bin / bash
    ### BEGIN INIT INFO
    # Início padrão: 2 3 4 5
    ### END INIT INFO

#### DECLARAÇÃO DA POLÍTCA PADRÃO - RESTRITIVA
    iptables -P INPUT DROP
    iptables -P OUTPUT DROP
    iptables -P FORWARD DROP

 #### LIMPAR AS REGRAS DAS CHAINS DA TABELA FILTRO E NAT
    iptables -F
    iptables -t nat -F

#### HABILITAR ROTEAMENTO
    echo 1> / proc / sys / net / ipv4 / ip_forward
    # HABILITAR FUNCAO DE NAT
    iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE

#### REGRA | ESTADO DO PACOTE | PERMITINDO RETORNO DE PACOTE ####
    iptables -A INPUT -m state --state ESTABELECIDO, RELACIONADO -j ACEITAR
    iptables -A SAÍDA -m estado --estado ESTABELECIDO, RELACIONADO -j ACEITAR
    iptables -A FORWARD -m state --state ESTABELECIDO, RELACIONADO -j ACEITAR

#### LIBERAR O LOCALHOST | Baseado por IP - 127.0.0.1
    #iptables -A INPUT -s 127.0.0.1 -j ACEITAR
    #iptables -A SAÍDA -d 127.0.0.1 -j ACEITAR

#### BASEADO EM INTERFACE - lo
    iptables -A ENTRADA -i lo -j ACEITAR
    #iptables -A SAÍDA -o lo -j ACEITAR

 #### LIBERAR O ACESSO DO CLIENTE 
    #iptables -A INPUT -s 10.10.0.1 -j ACEITAR
    #iptables -A SAÍDA -d 10.10.0.1 -j ACEITAR
    #iptables -A FORWARD -s 10.10.0.1 -j ACEITAR
    #iptables -A FORWARD -d 10.10.0.1 -j ACEITAR

 #### LIBERAR SSH DO FIREWALL
    #iptables -A INPUT -p tcp --dport 22 -j ACEITAR
    #iptables -A SAÍDA -p tcp --sport 22 -j ACEITAR

 #### REJEITAR ICMP DO CLIENTE - GERAR LOG QUANDO ACIONADO
    iptables -A FORWARD -s 10.10.0.1 -d 172.31.0.253 -p icmp -j LOG --log-prefix "Tentativa frustrada de LOG"
    iptables -A FORWARD -s 10.10.0.1 -d 172.31.0.253 -p icmp -j REJEITAR

 #### LIBERAR COMPARTILHAMENTO DE ARQUIVO 
    iptables -A FORWARD -d 172.31.0.252 -p tcp -m multiport --dport 139.445 -j ACEITAR
    #iptables -A FORWARD -d 172.31.0.252 -p tcp -m multiport --sport 139.445 -j ACEITAR
    iptables -A FORWARD -d 172.31.0.252 -p tcp -m multiport --dport 137,138 -j ACEITAR
    #iptables -A FORWARD -d 172.31.0.252 -p tcp -m multiport --sport 137,138 -j ACEITAR

 #### LIBERAR ACESSO A INTERNET (NAVEGACAO): EXCETO SRVDC-NAIROBI
    iptables -A FORWARD! -s 172.31.0.252 -p tcp -m multiport --dport 80.443 -j ACEITAR
    #iptables -A FORWARD! -d 172.31.0.252 -p tcp -m multiport --dport 80.443 -j ACEITAR

 #### LIBERAR ICMP PARA TODA REDE
    iptables -A INPUT -p icmp -j ACEITAR
    iptables -A SAÍDA -p icmp -j ACEITAR
    iptables -A FORWARD -p icmp -j ACEITAR

 #### RESTRINGIR SSH PARA CLIENTE, SERVIDORES E INTERNET | Regra para o cliente
    iptables -A INPUT -s 10.10.0.1 -p tcp --dport 22 -j ACEITAR
    #iptables -A SAÍDA -d 10.10.0.1 -p tcp --sport 22 -j ACEITAR
 ##### Regra para servidores
    iptables -A INPUT -s 172.31.0.0/24 -p tcp --dport 22 -j ACEITAR
    #iptables -A SAÍDA -d 172.31.0.0/24 -p tcp --sport 22 -j ACEITAR
 ##### Regra para internet
    iptables -A ENTRADA -i enp0s3 -p tcp --dport 22 -j ACEITAR
    #iptables -A INPUT -o enp0s3 -p tcp --sport 22 -j ACEITAR

 #### LIBERAR PROTOCOLO DNS
    iptables -A FORWARD -p udp --dport 53 -j ACEITAR
    #iptables -A FORWARD -p udp --sport 53 -j ACEITAR
    iptables -A SAÍDA -p udp --dport 53 -j ACEITAR
    #iptables -A INPUT -p udp --sport 53 -j ACEITAR

 #### LIBERAR REPOSITORIO LINUX
    iptables -A SAÍDA -d deb.debian.org -j ACEITAR
    #iptables -A INPUT -s deb.debian.org -j ACEITAR
    iptables -A SAÍDA -d security.debian.org -j ACEITAR
    #iptables -A INPUT -s security.debian.org -j ACEITAR
    iptables -A FORWARD -d deb.debian.org -j ACEITAR
    #iptables -A FORWARD -s deb.debian.org -j ACEITAR
    iptables -A FORWARD -d security.debian.org -j ACEITAR
    #iptables -A FORWARD -s security.debian.org -j ACEITAR

 #### LISTAR A CONFIGURAÇÃO ATUAL
    Claro
    iptables -L -nv --line-numbers

-------------------------------------------------- -----------

# SCRIPT FINAL - ESTATÍSTICO

    #! / bin / bash
    ### BEGIN INIT INFO
    # Início padrão: 2 3 4 5
    ### END INIT INFO

#### DECLARAÇÃO DA POLÍTCA PADRÃO - RESTRITIVA
    iptables -P INPUT DROP
    iptables -P OUTPUT DROP
    iptables -P FORWARD DROP

#### LIMPAR AS REGRAS DAS CHAINS DA TABELA FILTRO E NAT
    iptables -F
    iptables -t nat -F

#### HABILITAR ROTEAMENTO
    echo 1> / proc / sys / net / ipv4 / ip_forward
    
#### HABILITAR FUNCAO DE NAT
    iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE

#### REGRA 0 | ESTADO DO PACOTE | PERMITINDO RETORNO DE PACOTE 
    iptables -A INPUT -m state --state ESTABELECIDO, RELACIONADO -j ACEITAR
    iptables -A SAÍDA -m estado --estado ESTABELECIDO, RELACIONADO -j ACEITAR
    iptables -A FORWARD -m state --state ESTABELECIDO, RELACIONADO -j ACEITAR

##### LIBERAR LOCALHOST
    iptables -A ENTRADA -i lo -j ACEITAR

#### REJEITAR ICMP DO CLIENTE - GERAR LOG QUANDO ACIONADO
    iptables -A FORWARD -s 10.10.0.1 -d 172.31.0.253 -p icmp -j LOG --log-prefix "Tentativa frustrada de LOG"
    iptables -A FORWARD -s 10.10.0.1 -d 172.31.0.253 -p icmp -j REJEITAR

#### LIBERAR COMPARTILHAMENTO DE ARQUIVO 
    iptables -A FORWARD -d 172.31.0.252 -p tcp -m multiport --dport 139.445 -j ACEITAR
    iptables -A FORWARD -d 172.31.0.252 -p tcp -m multiport --dport 137,138 -j ACEITAR

#### LIBERAR ACESSO A INTERNET (NAVEGACAO): EXCETO SRVDC_NAIROBI
    iptables -A FORWARD! -s 172.31.0.252 -p tcp -m multiport --dport 80.443 -j ACEITAR

#### LIBERAR ICMP PARA TODA REDE
    iptables -A INPUT -p icmp -j ACEITAR
    iptables -A SAÍDA -p icmp -j ACEITAR
    iptables -A FORWARD -p icmp -j ACEITAR

 #### RESTRINGIR SSH PARA CLIENTE, SERVIDORES E INTERNET
 ##### Regra para o cliente
    iptables -A INPUT -s 10.10.0.1 -p tcp --dport 22 -j ACEITAR
 ##### Regra para servidores
    iptables -A INPUT -s 172.31.0.0/24 -p tcp --dport 22 -j ACEITAR
 ##### Regra para internet
    iptables -A ENTRADA -i enp0s3 -p tcp --dport 22 -j ACEITAR

 #### LIBERAR PROTOCOLO DNS
    iptables -A FORWARD -p udp --dport 53 -j ACEITAR
    iptables -A SAÍDA -p udp --dport 53 -j ACEITAR

 #### LIBERAR REPOSITORIO LINUX
    iptables -A SAÍDA -d deb.debian.org -j ACEITAR
    iptables -A SAÍDA -d security.debian.org -j ACEITAR
    iptables -A FORWARD -d deb.debian.org -j ACEITAR
    iptables -A FORWARD -d security.debian.org -j ACEITAR

 #### LISTAR A CONFIGURAÇÃO ATUAL
    Claro
    iptables -L -nv --line-numbers
