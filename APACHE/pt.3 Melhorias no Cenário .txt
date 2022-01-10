AULA 05 - MELHORIAS NO CENÁRIO 1 - CONTINNUAÇÃO

PROCESSOS

    * TÓQUIO
    * BERLIM
    * DENVER

    DNS

    * Nome -> IP
    * Zona Direta e Zona reversa
    * Foward

----------------------------------------------

LIGUE TODOS OS SERVIDORES

    Execute o comando ./fireall.sh no SRVFW-BERLIM 
    para conectar com a internet

__________________________________________________________________________

   Alocar mais memória no WinXP para evitar travamentos

    OBS: configurações feitas no VirtualBox

    1) Desligue a máquina > Selecione a Vm > Configurações > Sistema > 1024 - RAM

__________________________________________________________________________

SRVWEB-DENVER

    1) Acesse o Denver pelo CLIXP

    2) Instale o serviço de DNS 
                   apt install bind9 bind9-doc dnsutils -y

        !Verificar se está ativo 
                   systemctl status bind9.service

        OBS: Para sair dos status de serviço aperte a tecla "q"

    3) Altere o arquivo nano ou vim /etc/bind/named.conf.local

//
// Do any local configuration here
//

// Consider adding the 1918 zones here, if they are not used in your
// organization
//include "/etc/bind/zones.rfc1918";

zone "projetos.lin.br" {
        type master;
        file "/etc/bind/db.projetos.lin.br";
};

zone "0.31.172.in-addr.arpa" {
        type master;
        file "/etc/bind/db.0.31.172";
};

    4) Digite o comando *named-checkconf* para verificar se contém erros no arquivo de configuração do bind

    5) Digite o comando 
                cp -vbf /etc/bind/db.local /etc/bind/db.projetos.lin.br

    6) Altere o arquivo com 
                 nano ou vim /etc/bind/db.projetos.lin.br

                 !Verificar o status emita *named-checkconf*
;
; BIND zone file projetos.lin.br
;
$TTL    604800
@       IN      SOA     projetos.lin.br. root.projetos.lin.br. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@               IN      NS      projetos.lin.br.
@               IN      A       172.31.0.254
SRVFW-BERLIM    IN      A       172.31.0.254
@               IN      A       172.31.0.253
SRVWEB-DENVER   IN      A       172.31.0.253
WWW             IN      CNAME   projetos.lin.br
@               IN      AAAA    ::1

    7) Digite o comando 
                  cp -vbf /etc/bind/db.127 /etc/bind/db.0.31.172

    8) Altere o arquivo 
                  nano ou vim /etc/bind/db.0.31.172
        
                  !Verificar o status emita *named-checkconf*

;
; BIND reverse ile projetos.lin.br
;
$TTL    604800
@       IN      SOA     projetos.lin.br. root.projetos.lin.br. (
                              1         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      projetos.lin.br.
0.254   IN      PTR     projetos.lin.br.
0.254   IN      PTR     SRVFW-BERLIM.projetos.lin.br
0.253   IN      PTR     SRVWEB-DENVER.projetos.lin.br

    9) Digite o comando 
                 nano ou vim /etc/bind/named.conf.options
 
                 !Verificar o status emita *named-checkconf*

acl goodclients {
        10.10.0.0/29;
        172.31.0.0/24;
        localhost;
};

options {
        directory "/var/cache/bind";

        // If there is a firewall between you and nameservers you want
        // to talk to, you may need to fix the firewall to allow multiple
        // ports to talk.  See http://www.kb.cert.org/vuls/id/800113

        // If your ISP provided one or more IP addresses for stable
        // nameservers, you probably want to use them as forwarders.
        // Uncomment the following block, and insert the addresses replacing
        // the all-0's placeholder.
        recursion yes;
        allow-query { goodclients; };

        forwarders {
                192.168.1.41;
                192.168.1.33;
                8.8.8.8;
        };
        forward only;

        //========================================================================
        // If BIND logs error messages about the root key being expired,
        // you will need to update your keys.  See https://www.isc.org/bind-keys
        //========================================================================
        dnssec-enable yes;
        dnssec-validation yes;
        auth-nxdomain no;       #conform to RFC1035

        listen-on-v6 { any; };
};

    10) Reinicie o serviço com 
                       systemctl restart bind9.service

        !              Verifique o status desse serviço com 
                                         systemctl status bind9.service

    11) Edite o arquivo nano ou vim /etc/resolv.conf

domain projetos.lin.br
search projetos.lin.br
nameserver 172.31.0.253

    12) Reinicie o DNS 
             'systemctl restart bind9.service'

______________________________________________________________________________

CLIXP

    1) Mude o DNS para 172.31.0.253 no CLIXP-TOQUIO

    2) Faça o teste no navegador com www.terra.com.br

    3) INSIRA o comando *nslookup srvfw-berlim ou nslookup srvweb-denver*
          NÃO PODE TER NENHUM ERRO

______________________________________________________________________________

IMPORTE - WindowsServer2008R2_DC

    1) Características da Vm

        Nome: SRVDC-NAIROBI
        A placa de rede deve estar desmarcada no momento da importação!

    2) Configurações no VirtualBox para o SRVDC-NAIROBI

        Geral > Básico > Versão > Windows 2008 x64 (64 bits)

        SISTEMA (RAM) - 2048 MB

        MONITOR - 128MB (VBoxSVGA)

        ÁUDIO - desabilitado

        PLACA DE REDE - Rede Interna > REDE_SRV

    3) Iniciar a máquina

    4) Ao iniciar a máquina utilize a tela em modo normal e não em modo escalonado

        * Entrada > Inserir Ctrl-Alt-Del

    5) Logue com o Administrador 

        Senha: Senai@132

    6) Quando aparecer a mensagem para reiniciar a máquina feche essa aba.
       !Logo após, desligue a máquina

            * Start > Clique na seta ao lado de 'Log off' > Shutdown > Hardware Installation Planned > OK

    7) Adicione um novo disco óptico ao Servidor

        - Desligue a máquina
        - selecione a máquina > Configurações > Armazenamento > Adicionar novo disco óptico > Deixar vazio

    8) Ao iniciar a máquina utilize a tela em modo normal e não em modo escalonado

        Clique em Dispositivo > Inserir imagem de CD...

        OBS: Lembre-se da etapa 4 (será executada toda vez que a máquina for ligada)

    9) Após fechar a aba (etapa 6), uma mensagem referente ao novo disco surge

        - Clique na primeira opção que aparecer
        - Siga a instalação com *next*
        - Confirme a opção de reboot

    10) Volta para a Vm para ativar as opções bi-direcionais
        
        Dispositivo > Área de Transferência Compartilhada > Bi-direcional
        Dispositivo > Arrastar e Soltar > Bi-direcional

        OBS: Lembre-se da etapa 4 (não aparecerá se o modo escalonado estiver ativo)

            Como sair do desse modo escalonado: Ctrl (direito) + C

    11) Pronto! 
        Desligue a máquina.