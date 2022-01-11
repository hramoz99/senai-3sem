NAT - PFSENSE - AULA 35 -- 20/09/21

    Firewall > NAT > Encaminhamento de Portas

        Configuração:

            * Interface: WAN
            * Protocolo: TCP
            * Endereço de origem: *
            * Portas de Origem: *
            * Endereço de Destino: WAN Address
            * Portas de Destino: 80 (HTTP)
            * IP NAT: 172.31.0.251
            * Portas NAT: 80 (HTTP)
            * Descrição: Acesso para o micro SRVMON-HELSINQUE

----------------------------------

No Win10

    1) Abra o navegador e digite 192.168.100.124/cacti

        NOTA: Lembre de ligar o HELSINQUE!
        Entre com suas credenciais

----------------------------------

SRVMON-HELSINQUE

    2) Altere a porta ssh para 2222
        
        * vi /etc/ssh/sshd_config
            Linha 13
                Port 2222

        * Reinicie o serviço com
            systemctl restart sshd.service

        * Acesse o SRVMON-HELSINQUE pelo Putty ou MobaxTerm pela porta 2222

ACESSO SSH

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

REDIRECIONAMENTO DE PORTAS

    172.31.0.253 (DENVER) ----> 2221
    172.31.0.250 (MOSCOU) ----> 2223
