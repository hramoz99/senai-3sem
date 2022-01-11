# NAT - PFSENSE - 20/09/21

 **Firewall > NAT > Encaminhamento de Portas**

        CONFIGURAÇÃO:

            * Interface: WAN
            * Protocolo: TCP
            * Endereço de origem: *
            * Portas de Origem: *
            * Endereço de Destino: WAN Address
            * Portas de Destino: 80 (HTTP)
            * IP NAT: 172.31.0.251
            * Portas NAT: 80 (HTTP)
            * Descrição: Acesso ao micro 'SRVMON-HELSINQUE'

----------------------------------

**WINDOWS - Win10**

    1) Digite no navegador: 192.168.100.124/cacti

        NOTA: 'Ligar o HELSINQUE'
       
----------------------------------

**SRVMON-HELSINQUE**

    2) Alterar a porta ssh para 2222
        
        * vi /etc/ssh/sshd_config
            Linha 13
                Port 2222

        * Reiniciar o serviço 
            'systemctl restart sshd.service'

        * Acessear micro SRVMON-HELSINQUE pelo Putty

**ACESSO SSH**

    Firewall > NAT > Encaminhamento de Portas

        * Interface: WAN
        * Protocolo: TCP
        * Endereço de origem: *
        * Portas de Origem: *
        * Endereço de Destino: WAN Address
        * Portas de Destino: 2222
        * IP NAT: 172.31.0.251
        * Portas NAT: 2222
        * Descrição: Acesso externo ao SRVMON-HELSINQUE

----------------------------------

**REDIRECIONAMENTO DE PORTAS**

    172.31.0.253 (DENVER) ----> 2221
    172.31.0.250 (MOSCOU) ----> 2223
