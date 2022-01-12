> LINKS:
    https://cybermap.kaspersky.com/
    https://www.digitalattackmap.com/

*NOTA: Por padrão as configurações do IPtables são gravados na memória RAM* 
     
     Arquivo criado "./firewall.sh" 

# COMANDOS 

 * iptables -L
        
        <> Listar conteúdo da tabela filter

  * iptables -L -v
        
        <> Listar nomes

  * iptables -L -v -n (-nv)
        
        <> Listar apenas por IP

   * iptables -L -nv --line-numbers
        
         <> Listar numerando as linhas

   * iptables -D [INPUT-OUTPUT-FORWARD] [número-da-linha]
        
          <> Apagar linha determinada 

---------------------------------------------------------

# SCRIPT - FIREWALL

 ### MÁQUINA VIRTUAL

    1) Criar um arquivo vazio (Local onde todas as declarações de políticas e regras internamente serão adicionadas)
        

    2) Edite o FIREWALL	

         #! / bin / bash
         ## DECLARAÇÃO DE POLÍTCA RESTRITIVA
         iptables -P INPUT DROP
         iptables -P OUTPUT DROP
         iptables -P FORWARD

    3) Modificar o arquivo para executável
        'chmod + x firewall'

    4) Execute o arquivo
        ./firewall
        iptables -L

    5) Criar uma exceção para a outra Máquina - sem arquivo "firewall"

        #! / bin / bash
        ## DECLARAÇÃO DE POLÍTCA RESTRITIVA
        iptables -P INPUT DROP
        iptables -P OUTPUT DROP
        iptables -P FORWARD

        ## LIBERAR O ACESSO AO CLIENTE 
        iptables -A INPUT -s 10.10.0.1 -j ACCEPT
        iptables -A SAÍDA -d 10.10.0.1 -j ACCEPT
        iptables -A FORWARD -s 10.10.0.1 -j ACCEPT
        iptables -A FORWARD -d 10.10.0.1 -j ACCEPT

           Execute o comando -> ./firewall
          Verificar o iptables -> iptables -L

    6) Apagar linhas (regras) repetidas no INPUT
        #iptables -D INPUT 2

-----------------------------------------------

# SCRIPT DE MELHORIAS DE NOSSO

    7) Volte no arquivo "firewall"

        #! / bin / bash
        ## DECLARAÇÃO DE POLÍTCA RESTRITIVA
        iptables -P INPUT DROP
        iptables -P OUTPUT DROP
        iptables -P FORWARD

#### LIMPAR AS CHAINS DA TABELA FILTER
        iptables -F

#### LIBERAR O ACESSO DO CLIENTE 
        iptables -A INPUT -s 10.10.0.1 -j ACEITAR
        iptables -A SAÍDA -d 10.10.0.1 -j ACEITAR
        iptables -A FORWARD -s 10.10.0.1 -j ACEITAR
        iptables -A FORWARD -d 10.10.0.1 -j ACEITAR  

 #### LISTAR A CONFIGURAÇÃO ATUAL
        Clear
        iptables -L -nv --line-numbers          
        
 > Execute o comando novamente -> ./firewall

-----------------------------------------------

# BOTÃO DE PÂNICo 
## LIMPAR TODAS AS CONDIÇÕES 


    8) Criar um arquivo vazio

    9) Torne o arquivo executável
        chmod + x pânico

    10) Edite o arquivo

        #! / bin / bash

 #### DECLARAR A POLÍTICA PADRÃO PERMISSIVA
        iptables -P INPUT ACCEPT
        iptables -P SAÍDA ACEITAR
        iptables -P FORWARD ACCEPT

 #### LIMPAR AS CHAINS DA TABELA FILTER
        iptables -F

 #### LIMPAR A CONSOLE E APRESENTAR CONFIGURAÇÃO ATUAL
        Clear
        iptables -L -nv

-----------------------------------------------

> NOTA: Interface de loopback (localhost) é bloqueado na política restritiva

-----------------------------------------------

#### LIBERAR O LOCALHOST (sem arquivo firewall)

        #! / Bin / bash
        ## DECLARAÇÃO DE POLÍTCA RESTRITIVA
        iptables -P INPUT DROP
        iptables -P OUTPUT DROP
        iptables -P FORWARD

#### LIMPAR AS CHAINS DA TABELA FILTER
        iptables -F

#### LIBERAR O LOCALHOST
        Baseado por IP - 127.0.0.1
        iptables -A INPUT -s 127.0.0.1 -j ACEITAR
        iptables -A SAÍDA -d 127.0.0.1i -j ACEITAR

#### BASEADO NA INTERFACE - lo
        iptables -A ENTRADA -i 127.0.0.1 -j ACEITAR
        iptables -A SAÍDA -o 127.0.0.1i -j ACEITAR

#### LIBERAR O ACESSO DO CLIENTE
        iptables -A INPUT -s 10.10.0.1 -j ACEITAR
        iptables -A SAÍDA -d 10.10.0.1 -j ACEITAR
        iptables -A FORWARD -s 10.10.0.1 -j ACEITAR
        iptables -A FORWARD -d 10.10.0.1 -j ACEITAR  

 #### LISTAR A CONFIGURAÇÃO ATUAL
        Claro 
        iptables -L -nv --line-numbers

-----------------------------------------------

## REINICIE A MÁQUINA

    12) init 6
        Veja que configurações de firewall foram apagadas

-----------------------------------------------

## AUTOMAÇÃO DO SCRIPT ->  inicialização do Sistema

    NOTA:
        No ./firewall

            #! / bin / bash
            ### BEGIN INIT INFO
            # Início padrão: 2 3 4 5
            ### END INIT INFO
    
    13) Navegue para o arquivo 
              'cd / etc / systemd / system'

    14) Crie um arquivo vazio
        #touch firewall.service

    15) Edite o arquivo

        [Unidade]
        Descrição = Firewall

        [Serviço]
        Tipo = bifurcação
        ExecStart = / etc / init.d / firewall start

        [Instalar]
        WantedBy = multi-user.target

    16) Voltar ao caminho anterior 
        #CD 

    17) Vá até o diretório "/" e mova o arquivo "firewall"
        #CD /
        #mv / root / firewall /etc/init.d/

    18) Habilite o arquivo
        systemctl enable firewall.service

-----------------------------------------------

ARQUIVO DE FIREWALL

    19) Origem /etc/init.d

-----------------------------------------------

DESAFIO

 * LIBERAR O ACESSO SSH DO FIREWALL
 * LIBERAR O ICMP PARA TODA REDE

SOLUÇÃO
    
#### LIBERAR SSH DO FIREWALL
    iptables -A INPUT -p tcp --dport 22 -j ACEITAR
    iptables -A SAÍDA -p tcp --sport 22 -j ACEITAR


#### LIBERAR ICMP PARA TODA CENÁRIO
    iptables -A INPUT -p icmp -j ACEITAR
    iptables -A SAÍDA -p icmp -j ACEITAR
    iptables -A FORWARD -p icmp -j ACEITAR
