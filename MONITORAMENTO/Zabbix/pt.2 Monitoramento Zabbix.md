# MONITORAMENTO COM ZABBIX - INSTALAÇÃO (20/08)


 ### Instalar o Banco de Dados MySQL 5.7

     Validador de chaves
       #apt install gnupg -y

         Pacote de repositório
           #wget https://dev.mysql.com/get/mysql-apt-config_0.8.13-1_all.deb   

              Instalar pacote
                #dpkg -i mysql-apt-config_0.8.13-1_all.deb

                         1) OK
                         2) Primeira opção (MySQL Server & Cluster ...)> mysql-5.7
                         3) Primeiro OK

      Atualizar pacotes
        # apt update

           Instalação do servidor
               #apt install mysql-server
               ! Criação da senha do banco de dados: *******

                Validar o status do serviço
                #systemctl status mysql.service

           Próximas etapas: Site 'zabbix.org'

               Baixar o arquivo do repositório do Zabbix
                 #wget https://repo.zabbix.com/zabbix/5.0/debian/pool/main/z/zabbix-release/zabbix-release_5.0-1+buster_all.deb

                 Instalação do pacote
                   #dpkg -i zabbix-release_5.0-1 + buster_all.deb

                   Atualizar os pacotes
                     # apt update

                 Instalar o servidor Zabbix
                       #apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-agent

             Configurar o banco de dados MySQL ao Zabbix
              #mysql -uroot -p
               mysql> criar banco de dados e conjunto de caracteres zabbix utf8 agrupar utf8_bin;
               mysql> criar usuário zabbix @ localhost identificado por 'Senai @ 132';
               mysql> conceder todos os privilégios no zabbix. para zabbix @ localhost;
               mysql> quit;

             Inserir esquema ao banco de dados
              #zcat /usr/share/doc/zabbix-server-mysql*/create.sql.gz | mysql -uzabbix -p zabbix

             Informar a senha do banco de dados no arquivo de configuração do Servidor Zabbix
              # / etc / zabbix / zabbix_server.conf
                    Linha 124: descomentar e inserir senha
                        DBPassword = **********
                
             Alterar fuso horário sem PHP
               #vim /etc/zabbix/apache.conf
                  Linha 20 e 30: descomentar e ajustar para América / São_paulo

             Reiniciar e Habilitar os serviços disponíveis
               #systemctl restart zabbix-server zabbix-agent apache2
               #systemctl enable zabbix-server zabbix-agent apache2

              Finalizar a instalação do Zabbix pelo navegador
                  http: // (ip-host-only / zabbix / setup.php
                        Exemplo: http://192.168.56.101/zabbix/setup.php

                     - Insira a senha do Banco de Dados - Senai @ 132
                     - Insira o nome do Banco de Dados - SRVMON-MOSCOU

                  Ajuste para a instalação final
                    Caminho: /usr/share/zabbix/conf/zabbix.conf.php

                  Criação  arquivo vazio
                    #touch /usr/share/zabbix/conf/zabbix.conf.php

                   Ajuste da propriedade do arquivo para o Apache2
                    #chown www-data /usr/share/zabbix/conf/zabbix.conf.php

                Acessar o Zabbix
                    Usuário: Admin
                    Senha: zabbix
