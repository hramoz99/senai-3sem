PERSONALIZANDO (25/08))

INVENTÁRIO

    Criação de um novo item : 
        Configuração> Hosts> SRVFW-BERLIM (ou outro dispositivo)> Itens> Criar item)
        
          Documentação: 
            - https://www.zabbix.com/documentation/5.0/pt/manual/config/items/item
            - https://www.zabbix.com/documentation/5.0/pt/manual/config/items/itemtypes/zabbix_agent

        Criação de itens para o 'Inventario' 

            - Inventário - MAC
                system.hw.macaddr [enp0s3, full]
                  Tipo de informação: Texto
                    Aplicativo: Inventario 
             ! Caso não tenha, coloque 'Novo aplicativo'
                Campos Populares do inventário (HOST): 
                * ADICIONAR endereço MAC A
                * Voltar em Configuração> Hosts> Dispositivo> Itens> Inventário
                * Selecionar o item criado> Final da tela> Executar AGORA

          NOTA: Configuração> Hosts> Dispositivo> Inventário> Clique em "Automático"

            - Inventario - Pacotes
                system.sw.packages [all, all, full]

            - Inventario - OS
                system.sw.os [completo]

-------------------------------------------------- ------------

FILTRO DE INFORMAÇÕES - Como saber se o usuário final alterou o DNS?

    Visualição do DNS - RESOLVER
        cat /etc/resolv.conf
        cat /etc/resolv.conf | grep nameserver
        cat /etc/resolv.conf | grep nameserver | cut -d "" -f2

    No Zabbix
        system.run [cat /etc/resolv.conf | grep nameserver | cut -d "" -f2]
        Aplicativo de software A

         Erro: Comandos remotos não habilitados ...

            SRVFW-BERLIM
                #cd / etc / zabbix
                #vim zabbix_agentd.conf
                    Linha 73 - Descomentar e trocar o 0 por 1
                #systemctl restart zabbix_agent.service

        Execute o item novamente 
        ! Clique em 'Detalhes' (Inventário> Hosts> SRVFW-BERLIM> Detalhes)

-------------------------------------------------- ------------

VIZUALIÇÃO DAS INFORMAÇÕES 

    Monitoramento> Dados mais recentes

 

-------------------------------------------------- ------------

VERIFICAÇÃO DO APACHE - SRVWEB-DENVER

    1) Item de Criação de "Verificação Apache2"
        net.tcp.service [serviço, <ip>, <port>]
            net.tcp.service [http ,, 80]
        
        Tipo de informação - Numérica (sem sinal)
         Novo aplicativo - Serviços

        ! Faça o teste enxerrando o serviço

    2) Crie um novo gatilho - Mostrar quando a porta parar
        Configuração> Hosts> SRVWEB-DENVER> Triggers> Criar 'Trigger'

            Nome: Serviço WEB fora do ar
            Gravidade - Desastre

            Expressão> Adicionar
                Doença
                   {SRVWEB-DENVER: net.tcp.service [http ,, 80] .sum (60)} = 0

            Descrição
                Quando o serviço WEB estiver fora do ar (condição 0), o Zabbix alarmará como "Desastre"

        Faça o teste iniciando o serviço

    3) Resolva este problema indo em
        Monitoramento> Problemas
            Ack - Não
                Problema de atualização
                    Mensagem: Manutenção prevista e realizada

                    Mudança de gravidade - Marcar 'Unacknowledge'

-------------------------------------------------- ------------

BIBLIOTECA ITIL

    Incidentes eventuais em um curto período de tempo pode se tornar um problema
        EXEMPLO: Apache caiu três vezes no mesmo dia

-------------------------------------------------- ------------

GIRAR

    Rotação de log
        Syslog1 - até 100MB, enviar uma informação para Syslog2
        Syslog2 - até 500MB, enviar uma informação para Syslog3
        .
        .
        .
        Syslogn - até X, enviar uma informação para Syslogn

-------------------------------------------------- ------------

AÇÕES - ZABBIX
    Configuração> Ações> Criar ações

        Nome: Reiniciar o serviço WEB
        Doença  
            Tipo - gatilho
            Triggers - Serviço WEB fora do ar

    Operação
            Comando remoto
            Script personalizado - agente Zabbix
                sudo / bin / systemctl restart apache2.service

PERMISSÃO AO USUÁRIO DO ZABBIX 

    #apt update
    #apt install sudo
    #vim / etc / sudoers
        Linha 21
            zabbix ALL = NOPASSWD: / bin / systemctl restart apache2.service, / bin / kill
            : wq!

    #vim / etc / passwd
        Linha 32
            zabbix: x: 108: 115 :: / inexistente: / bin / bash

    #cd / etc / zabbix
        #vim zabbix_agentd.conf
                    Linha 73
                        Descomentar e trocar 0 por 1
    #systemctl restart zabbix_agent.service

TESTE ESSA AUTOMAÇÃO

    1) Parar o apache2 
        'systemctl stop apache2.service'

    2) Alt + f6 (verificação do log em outra janela)
        #tail -f -n 1000 / var / log / syslog

    3) Patch - mensagem que o serviço encerrou
        * É nesse momento que nossa automação resolverá este problema

CURIOSIDADE

	* https://techexpert.tips/pt-br/zabbix-pt-br/zabbix-monitorar-arquivo-de-log-no-linux/   
	* https://www.zabbix.com/documentation/current/pt/manual/config/items/itemtypes/log_items