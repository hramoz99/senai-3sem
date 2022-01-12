# OTIMIZAÇÃO DO CENÁRIO  pt.2 

**Processos - Debian (Linux) | Importação**

  * IP
  * Hostname
  * Acesso a internet
  * InstalaÇÃO dos pacotes 
  * Atualizar as configurações do servidor
     

--------------------------------------------------

**VERIFICAÇÃO - CLIXP & SRVFW-BERLIM**

    1) Iniciar as 3 máquinas

    2) Conectar no SRVFW-BERLIM por meio do CLIXP-TOQUIO (SSH)
       

    3) Digitar o comando './firewall.sh'

    4) CLIXP - ping os endereços

        ping 10.10.0.6
        ping 172.31.0.253
        ping 172.31.0.254

    5) Baixar o mobaxterm (versão portable)
          https://mobaxterm.mobatek.net/download-home-edition.html

--------------------------------------------------

**DENVER**

    1) Emitir o comando 'apt update - atualiza os pacotes de serviço'
                      

    3) Emitir o comando no terminal "apt install apache2 -y" - instalação do Apache
        
     
      
**SERVIDOR WEB**

            <> HTTP
                /var/www/html (caminho dos nossos sites)

        <> APACHE

            * Configurações
            * /etc/apache2

       <>  DNS

            * Nome

    4) Teste de ping 
            172.31.0.253

    5) Cópia do arquivo de configuração
        cp -vbf /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/site.conf

    6) Alterar o arquivo - 'nano ou vim /etc/apache2/sites-available/site.conf'

       Aparência do arquivo
 _______________________________________________________________________________________________
        
**VirtualHost**
```

  #The ServerName directive sets the request scheme, hostname and port that
  #the server uses to identify itself. This is used when creating
  #redirection URLs. In the context of virtual hosts, the ServerName
  #specifies what hostname must appear in the request's Host: header to
  #match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.
        ServerName www.projetos.lin.br
```
___________________________________________________________________________________________


      <> serverAdminwebmaster@Localhost          
            DocumentRoot /var/www/html/site

        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
        # error, crit, alert, emerg.
        # It is also possible to configure the loglevel for particular
        # modules, e.g.
        #LogLevel info ssl:warn

        ErrorLog ${APACHE_LOG_DIR}/error.site.log
        CustomLog ${APACHE_LOG_DIR}/access.site.log combined

        # For most configuration files from conf-available/, which are
        # enabled or disabled at a global level, it is possible to
        # include a line for only one particular virtual host. For example the
        # following line enables the CGI configuration for this host only
        # after it has been globally disabled with "a2disconf".

    7) Reiniciar o serviço  
             'systemctl restart apache2.service'
 
                    ! Verificar o status do serviço
                          'systemctl status apache2.service'


    8) Criação de um diretório 
             mkdir /var/www/html/site

    9) Editar o arquivo 'nano ou vim /var/www/html/site/index.html'

        <html>Site da Escola SENAI de Informatica - SEU NOME<html>

    10) Reiniciar o serviço apache2 
                'systemctl restart apache2.service'

                        ! Verificar o status do serviço
                              'systemctl status apache2.service'

    11) DIGITAR o comando  "a2ensite site.conf" - habilitar a página na internet

    12) DESABILITE o site padrão 
                 "a2dissite 000-default.conf"

    13) Reiniciar o serviço apache2 
                  'systemctl restart apache2.service'

    14) TESTE:
        abra o navegador do CLIXP e insira o IP 172.31.0.253

 **INFORMAÇÕES DE LOG**

        cat /var/log/apache2/error.site.log (Os erros do site aparecerão aqui)
        cat /var/log/apache2/access.site.log (Auditoria do site)

--------------------------------------------------

**MATERIAL DE APOIO**

    https://www.youtube.com/watch?v=ACGuo26MswI 

    https://www.youtube.com/watch?v=cRneZs9Lvno

    https://www.youtube.com/watch?v=epWv0-eqRMw
