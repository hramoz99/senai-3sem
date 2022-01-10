PRÁTICA - SINTAXE IPTABLES

    #iptables -> v1.8.2

    #iptables -t filter -L
        ! Listar as opções presentes na tabela "filter" (padrão) -> iptables -L

    #iptables -P INPUT DROP
        ! Sem entrada ao Firewall (sem ping) -> Entrar

    #iptables -P FORWARD DROP
        ! Sem entrada e saída do SRVFW-BERLIM -> Passar

  NOTA: Nestas duas situações o pacote é enviado da máquina, mas não volta (INPUT)

    #iptables -L -v

    #iptables -P OUTPUT DROP
        
  NOVA REGRA (Exceção da política -> Ping do cliente ou firewall)

        1) #iptables -A ENTRADA -s 10.10.0.1 -j ACEITAR
           #iptables -A SAÍDA -d 10.10.0.1 -j ACEITAR