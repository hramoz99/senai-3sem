Continuação -- PFSENSE - 17/09 (Continuação da aula do dia 16/09)

ORGANIZAÇÃO CENÁRIO

    * Alteração do Adaptador1 em modo NAT para modo Bridge
        Interface WAN - IP: 192.168.100.1xx (xx = ID da sessão do Anydesk)
            Exemplo: 192.168.100.124

        Sequência
            2
            1
            n
            192.168.100.124
            16
            192.168.1.1
            n
            enter
            enter

------------------------------------

DASHBOARD PFSENSE

    1) Criação de Grupos de IPs
        Firewall > Aliases > IP >  Add

        - Nome: Grupo_IP
        - Descrição: Faixa de IP de TI
        - Tipo: Host(s)
        - IP ou FQDN: 10.10.0.1 --> Lucas Cabral
        -             10.10.0.2

    2) Criação de Grupos de Portas
        Firewall > Aliases > Portas >  Add

        - Nome: Grupo_portas
        - Descrição: Selecionando portas que vamos liberar
        - Tipo: Porta(s)
        - Porta: 80 (HTTP), 53 (DNS), 20 (FTP), 21 (FTP_ATIVO), 22 (SSH), 25 (SMTP)

    3) Visualiação das regras
        Firewall > Regras

        - Podemos copiar as regras, movimenta-las (para definição de prioridade)
