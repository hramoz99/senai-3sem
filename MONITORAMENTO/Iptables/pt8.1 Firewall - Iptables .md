# SCRIPT
```
    #! / bin / bash
    ### BEGIN INIT INFO
    # Início padrão: 2 3 4 5
    ### END INIT INFO
```

#### POLÍTCA PADRÃO - RESTRITIVA
```
    iptables -P INPUT DROP
    iptables -P OUTPUT DROP
    iptables -P FORWARD DROP
```
#### LIMPAR AS REGRAS DAS CHAINS - TABELAS FILTER E NAT
```
    iptables -F
    iptables -t nat -F
```
#### HABILITAR ROTEAMENTO
```
    echo 1> / proc / sys / net / ipv4 / ip_forward
```
####  HABILITAR FUNCAO DE NAT
```
    iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE
```

#### STATEFUL ####
```
    iptables -A INPUT -m state --state ESTABELECIDO, RELACIONADO -j ACEITAR
    iptables -A SAÍDA -m estado --estado ESTABELECIDO, RELACIONADO -j ACEITAR
    iptables -A FORWARD -m state --state ESTABELECIDO, RELACIONADO -j ACEITAR
```
#### LIBERAR LOCALHOST
```
    iptables -A ENTRADA -i lo -j ACEITAR
```
#### REJEITAR ICMP DO CLIENTE - GERANDO LOG QUANDO ACIONADO
```
    iptables -A FORWARD -s 10.10.0.1 -d 172.31.0.254 -p icmp -j LOG --log-prefixo "CLI7WIN-TOQUIO realizou teste de ping neste servidor, estado: permissão negada"
    iptables -A FORWARD -s 10.10.0.1 -d 172.31.0.254 -p icmp -j REJEITAR
```
#### LIBERAR ACESSO A INTERNET (NAVEGACAO): EXCETO SRVWEB-DENVER
```
    iptables -A FORWARD! -s 172.31.0.253 -p tcp -m multiport --dport 80.443 -j ACEITAR
```
#### LIBERAR ICMP PARA TODA REDE
```
    iptables -A INPUT -p icmp -j ACEITAR
    iptables -A SAÍDA -p icmp -j ACEITAR
    iptables -A FORWARD -p icmp -j ACEITAR
```
#### LIBERAR O PROTOCOLO DE DNS (RESOLUÇÃO DE NOMES)
```
    iptables -A FORWARD -p udp --dport 53 -j ACEITAR
    iptables -A SAÍDA -p udp --dport 53 -j ACEITAR
```

#### LIBERAR O REPOSITÓRIO BRASILEIRO DO DEBIAN (LINUX)
```
    iptables -A SAÍDA -d mirror.unesp.br -j ACEITAR
    #iptables -A SAÍDA -d debian.pop-sc.rnp.br -j ACEITAR
    #iptables -A SAÍDA -d debian.itsbrasil.net -j ACEITAR
    iptables -A FORWARD -d mirror.unesp.br -j ACEITAR
    #iptables -A FORWARD -d debian.pop-sc.rnp.br -j ACEITAR
    #iptables -A FORWARD -d debian.itsbrasil.net -j ACEITAR
 ```   
#### LISTAR A CONFIGURAÇÃO ATUAL
```
    Clear
    iptables -L -nv --line-numbers
```
