# FIREWALL REGRAS- 02/09

### SOLUÇÃO

#### REJEITAR ICMP DO CLIENTE - GERANDO LOG QUANDO ACIONADO
    iptables -A FORWARD -s 10.10.0.1 -d 172.31.0.253 -p icmp -j REJEITAR
    iptables -A FORWARD -s 10.10.0.1 -d 172.31.0.253 -p icmp -j LOG --log-prefix "Tentativa de frustrada de LOG"

        NOTA: Mais restritivo em primeiro!

#### LIBERAR COMPARTILHAMENTO DE ARQUIVO
    iptables -A FORWARD -d 172.31.0.252 -p tcp -m multiport --dport 139.445 -j ACEITAR
    iptables -A FORWARD -d 172.31.0.252 -p tcp -m multiport --sport 139.445 -j ACEITAR
    iptables -A FORWARD -d 172.31.0.252 -p udp -m multiport --dport 137,138 -j ACEITAR
    iptables -A FORWARD -d 172.31.0.252 -p tcp -m multiport --sport 137,138 -j ACEITAR

        * Portas: 139, 445 (tcp) | 137, 138 (udp)

#### LIBERAR ACESSO A INTERNET (NAVEGAÇÃO): EXCETO SRVDC-NAIROBI
    iptables -A FORWARD! -s 172.31.0.252 -p tcp -m multiport --dport 80.443 -j ACEITAR
    iptables -A FORWARD! -d 172.31.0.252 -p tcp -m multiport --sport 80.443 -j ACEITAR

------------------------------------

### TIPOS DE FIREWALL

* Stateless -> sem estado ( do inicio até o fim)
* Stateful -> estado do pacote (neste caso, não é preciso garantir o retorno de)

#### REGRA 0 | ESTADO DO PACOTE | PERMITINDO RETORNO DE TODOS PACOTES COM ENVIO LIBERADO
    iptables -A INPUT -m state --state ESTABELECIDO, RELACIONADO -j ACEITAR
    iptables -A SAÍDA -m estado --estado ESTABELECIDO, RELACIONADO -j ACEITAR
    iptables -A FORWARD -m state --state ESTABELECIDO, RELACIONADO -j ACEITAR

       
