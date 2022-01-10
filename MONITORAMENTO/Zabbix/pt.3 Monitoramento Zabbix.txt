MONITORAMENTO DE HOSTS (RT / SW) - ITENS E INVENTÁRIO (23/08)

    INSTALAÇÃO DO AGENTE - LINUX

      1) No Painel de gerenciamento do Zabbix, vá em:
         Configuração> hosts> Criar host

          * Alterar o IP e o hostname do "Zabbix Server"
          * Criar um agente para o SRVFW-BERLIM & SRVWEB-DENVER

     Depois da instalação
        #apt install zabbix-agent

    Ajustes no arquivo 'zabbix-agentd.conf (#cd / etc / zabbix)'

            * Linha 98 (Agente) ou 117 (Servidor): informar o servidor de monitoramento - modo passivo
                Server = 172.31.0.250

            * Linha 139 (Agente) ou 158 (Servidor): informar o servidor de monitoramento - modo ativo
                ServerActive = 172.31.0.250

            * Linha 148 (Agente) ou 169 (Servidor): descomentar e informar o nome do host
                Hostname = NOME_DO_DISPOSITIVO
                Nome do host = SRVFW-BERLIM

    Reiniciar o serviço | Verificar funcionalidade
        #systemctl restart zabbix-agente.service
        #systemctl status zabbix-agente.service
        #ss -ntpl
        #zabbix_agentd -p | mais

--------------------------------------------------------------


   INSTALAÇÃO DO AGENTE - WINDOWS

       https://www.zabbix.com/download_agents?version=5.0+LTS&release=5.0.14&os=Windows&os_version=Any&hardware=amd64&encryption=No+encryption&packaging=Archive&show_legacy=0
       1) Win> Any> amd64> 5.0 LTS> Sem criptografia> Arquivo
             Download - https://cdn.zabbix.com/zabbix/binaries/stable/5.0/5.0.14/zabbix_agent-5.0.14-windows-amd64.zip

          NOTA: 'Lembrar de inserir o disco para que tenha uma integração com o seu pc raíz'

       2) Salvar a pasta no diretório 'Downloads'

       3) No diretório raíz crie uma pasta "Zabbix"
          Mova os conteúdos das pastas bin e conf para a pasta Zabbix

       4) Emita o comando como admin (sem cmd)
        c: \ zabbix \ zabbix_agentd.exe -cc: \ zabbix \ zabbix_agentd.conf -i
    
       5) Iniciar o serviço 
          services.msc > Zabbix.agent

       6) Verificar funcionakidade do serviço
        netstat -na | mais (sem cmd) 
        c: \ zabbix \ zabbix_agentd.exe -p