# OTIMIZAÇÃO DI CENÁRIO pt.2

## PROCESSOS

  * TÓQUIO
  * BERLIM
  * DENVER

**DNS**

   * Nome -> IP
   * Zona Direta e Zona reversa
   * Foward

----------------------------------------------

    Executar o comando ./fireall.sh <SRVFW-BERLIM> para conectar com a internet

__________________________________________________________________________

**Alocar mais memória - WinXP**

> OBS: configurações feitas no VirtualBox

    1) Desligar a máquina > Selecione a Vm > Configurações > Sistema > 1024 - RAM

__________________________________________________________________________

**SRVWEB-DENVER**

    1) Acessar a máquina "Denver" por SSH

    2) Instalar o serviço de DNS 
                   'apt install bind9 bind9-doc dnsutils -y'
                   

    3) Alterar o arquivo 
           'nano ou vim /etc/bind/named.conf.local'
```     
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
```  

    4) Digitar o comando 'named-checkconf' para verificar se há erros no arquivo de configuração bind

    5) Digitar o comando 
                'cp -vbf /etc/bind/db.local /etc/bind/db.projetos.lin.br'

    6) Alterar o arquivo 
                 'nano ou vim /etc/bind/db.projetos.lin.br'

```
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
```

    7) Digitar o comando 
                  'cp -vbf /etc/bind/db.127 /etc/bind/db.0.31.172'

    8) Alterar o arquivo 
                  'nano ou vim /etc/bind/db.0.31.172'
        
      ! Verificar o status emita *named-checkconf*
```
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
```
    
    9) Digitar o comando 
                 'nano ou vim /etc/bind/named.conf.options'
 
                
```
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

    10) Reiniciar o serviço 
                       'systemctl restart bind9.service'


    11) Editar o arquivo 
         'nano ou vim /etc/resolv.conf'

domain projetos.lin.br
search projetos.lin.br
nameserver 172.31.0.253

    12) Reiniciar o DNS 
             'systemctl restart bind9.service'
``` 
______________________________________________________________________________


**CLIXP**

    1) Configurar o DNS para 172.31.0.253

    2) Teste no navegador com www.terra.com.br

    3) INSIRA o comando nslookup srvfw-berlim 
                            ou 
                        nslookup srvweb-denver
          

______________________________________________________________________________

**IMPORTE - WindowsServer2008R2_DC**

    1) Características da Vm

        Nome: SRVDC-NAIROBI
        <> Placa de rede deve estar desmarcada no momento da importação!

    2) Configurações no VirtualBox 

        Geral > Básico > Versão > Windows 2008 x64 (64 bits)

        SISTEMA (RAM) - 2048 MB

        MONITOR - 128MB (VBoxSVGA)

        ÁUDIO - desabilitado

        PLACA DE REDE - Rede Interna > REDE_SRV

    3) Iniciar a máquina

    4) Máquina - tela em modo normal e não escalonado

        * Entrada > Inserir Ctrl-Alt-Del

    5) Logue com o Administrador 

              Senha: Senai@132

    6) Ao aparecer a mensagem "reiniciar", feche a aba.
             ! Logo após, desligue a máquina

            * Start > Clicar na seta 'Log off' > Shutdown > Hardware Installation Planned > OK

    7) Adicionar um novo disco óptico ao Servidor

        - Desligar a máquina
           <> Selecionar a máquina > Configurações > Armazenamento > Adicionar novo disco óptico > Deixar vazio

    8) Utilizar a tela em modo normal 

        Dispositivo > Inserir imagem de CD

    9) Nova mensagem - "novo disco surge"

        - Clicar na primeira opção 
        - Siga a instalação <next>
        - Confirmar a opção de 'reboot'

    10) Ativar as opções bi-direcionais na VM
        
        Dispositivo > Área de Transferência Compartilhada > Bi-direcional

  > NOTA: sair do modo escalonado: Ctrl (direito) + C

    11)  Desligue a máquina.
