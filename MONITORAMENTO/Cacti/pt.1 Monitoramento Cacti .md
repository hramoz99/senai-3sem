# MONITORAMENTO - PROTOCOLO SNMP 

 **CACTI**

     SNMP - Simple Network Management Protocol é o protocolo padrão para monitoramento e gerenciamento de redes.

____________________________________________

**SMI - Structure of Management Informatica**

     Define os campos ( tamanho (template))
     Codificação (gerente)

**MIB - Management Informatics Base**

     Define quais informações serão coletadas em cada Host;
     Modelo hierárquico

**SNMP - Simple Network Management Protocol**

     Todo dispositivo que receber IP na rede (e gerar informações) será considerado um agente (envia as informações)
     Gerente - Servidor Centralizado (solicita as informações)

       As informações serão dadas em texto puro / número
    ! Neste caso é utilizado um software (Zabbix, Cacti) para "traduzir" os dados
    
-----------------------------------------------

### AMBIENTE

     Importação VM

        - Nome: SRVMON-HELSINQUE
        - Gerar nova placa de rede
        - Desabilite o áudio
            - 128MB de vídeo (VMSVGA)
            - Placa de rede (Interna): REDE_SRV

        * IP - 172.31.0.251
        * Instalar o SSH
        * Apontamento do DNS (resol.conf)
          !Teste de ping 8.8.8.8, www.uol.com.br, 172.31.0.254 - Berlim

-----------------------------------------------

### PASSO A PASSO

    1) Iniciar a máquina SRVMON - HELSINQUE

    2) Acesse remotamente SRVMON-HELSINQUE pelo CLIXP-TOQUIO

    3) Execute os testes de ping

    4) Instalar os pacotes:
                   'apt install cacti cacti-spine rrdtool librrds-perl -y'
        
        - Selecionar "Apache2"
        - Configurar o banco de dados para o cacti com dbconfig = SIM
            !Senha para o banco de dados = SENAI#132 'Confirme a senha'

    5) Verificar dados do Apache : 
                       'dpkg -l apache2'

    7) Verificar as informações do banco de dados MariaDB:
                                         'dpkg -l mariadb-server-10.3'

    8) Editar o arquivo 'vim ou nano /etc/mysql/mariadb.conf.d/50-server.cnf'

    9) Colar as informações abaixo de '#MySQL/MariaDB default is'

     character-set-server = utf8mb4
     #collation-server = utf8mb4_general_ci
     collation-server = utf8mb4_unicode_ci
     character-set-server = utf8mb4
     innodb_flush_log_at_timeout = 4
     innodb_read_io_threads = 34
     innodb_write_io_threads = 17
     max_heap_table_size = 70M
     tmp_table_size = 70M
     join_buffer_size = 130M
     innodb_buffer_pool_size = 250M
     innodb_io_capacity = 5000
     innodb_io_capacity_max = 10000
     innodb_file_format = Barracuda
     innodb_large_prefix = 1

    10) Reiniciar os serviços:
         'systemctl restart mariadb.service'
           ! Verifique os status com systemctl status mariadb.service

    11) Verificar a versão do php:
        php -v

    12) Alterar o arquivo 'nano ou vim /etc/php/7.3/cli/php.ini'

    13) Coloque 'data.timezone = America/Sao_Paulo' na linha 954

    14) Altere o arquivo 'nano ou vim /etc/php/7.3/apache2/php.ini'

    15) Coloque *data.timezone = America/Sao_Paulo* na linha 956

    16) Reinicie o serviço de Apache:
         'systemctl restart apache2.service'
           ! Verifique o status com systemctl status apache2.service

    17) Intale o pacote 'apt install snmpd -y'

    18) Alterar o arquivo 'nano ou vim /etc/snmp/snmpd.conf'
        
        Linha 15: agentAddress udp:161
        Linha 51: rocommunity public default

    19) Reinicie o serviço:
         'systemctl restart snmpd.service'
           ! Verifique os status com systemctl status snmpd.service

    20) Emitir o comando 'snmpwalk -v2c -c public 172.31.0.251 | more'
         (As informações que serão traduzidas em um gráfico)
        
    21) Emitir o comando 'snmpwalk -v2c -c public 172.31.0.251 .1.3.6.1.2.1.1.1.0'
           ! Nome do Servidor e versão do Linux

-----------------------------------------------

    22) Endereço Web 172.31.0.251/cacti
        
        * Nome do usuário: admin
        * Senha: SENAI#132

-----------------------------------------------

### CACTI 

    23) Create Device > + 

         Características

            * Descrição: Servidor Cacti
            * Hostname: 172.31.0.251
            * Device Site Association: Core

               !Demais configuração: Padrão

    24) Adicionar novo template

            Console > Dispositivos (clique sobre o nome do dispositivo) > Editar

                Busque "Associated Graph Templates"

                    Add Graph Template > Unix - Ping Latency > Adicionar

-----------------------------------------------

### Instalação do pacote SNMP

    25) Painel de Controle > Programas padrão > Add or Remove Programs > Add/Remove Windows Components (lado esq da tela) > Management and Monitoring Tools > Next

    26) Ao chegar a mensagem para adicionar um disco, aperte o botão direito sob o disco que está em baixo da tela

    27) Escolher imagem de disco > C:\VMs\ISOs > en_windows_xp_professional_with_service_pack_3_x86_cd_vl_x14-73974

-----------------------------------------------

### Configuração do pacote SNMP

    30) Windows + R > services.msc 

    31) Clique 2x no 'SNMP Service' > Stop 

         Características

            AGENTE

                * Administrador.admin@projetos.win.br <Contato>
                * Sao Paulo - Matriz <Location>

            TRAPS
            
                * Public > Add > 172.31.0.251 - IP 

            SECURITY

                * Segunda opção- Accept SNMP packets from these hosts > Add > 172.31.0.251

        ! Inicie o serviço: Aply > OK > Start

    32) Criação de um novo Dispositivo no Cacti 

        * Descrição: CLIXP-TOQUIO
        * Hostname: 10.10.0.1
	* Generic SNMP

        OBS: Em caso de erro, desabilite o firewall do windows

**Introdução ao Gerenciamento de Redes - parte 4 - SNMP**

	(https://www.youtube.com/watch?v=PqgDoG4gLK0)
