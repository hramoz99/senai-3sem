AULA 04 - MELHORIAS NO CENÁRIO 1 

    SRVFW-BERLIM

    * Instalar o openssh
    * Instalar o vim
    * Acessar o nano ou vim /etc/network/interfaces

        Alterar o IP para 10.10.0.6
        Máscara: 255.255.255.248

    1) Reinicie as configurações de rede com

        systemctl restart networking.service

    2) Verificar o ssh (veja se está ativ0)

        systemctl status ssh.service

-----------------------------------------------

    ACESSE O WINXP

    1) Depois de adicionar um novo disco (Virtualbox)

        Altere as configurações de rede
          <
            IP: 10.10.0.1
            MASK: 255.255.255.248
            GW: 10.10.0.6
                          >
            *Teste de ping com GW*

   OBS: O ping para a internet falhará. 
   
   COMO ARRUMAR:

    2) Altere as informações para bi-direcional (Arrasta e Solta da Área de trabalho compartilhada)

-----------------------------------------------

    ACESSE O SRVFW-TOQUIO

    1) Escreva o comando

          echo 1 > /proc/sys/net/ipv4/ip_forward

    2) Coloque o comado
    
          iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE

-----------------------------------------------

    ACESSE O WINXP


    1) Faça o teste de ping com o dns do google

    2) Baixar o Putty (32bit)

          https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html

    3) Acessar o SRVFW-BERLIM pelo protocolo SSH

        Name: SRVFW-BERLIM
        IP: 10.10.0.6

              User: aluno
              Senha: Senai@132



    EM CASOS DE PROBLEMAS

        * Verificar se o usuário ALUNO existe
               
                 cat /etc/passwd | grep aluno


        * Mude a senha do aluno (opcional)

               passwd aluno

                 Nova senha:
                 Redigite a nova senha:

    4) Logar com o usuáio root

        su -
        Senha: Senai@132

    5) Altere o nome do SRV

         hostnamectl set-hostname SRVFW-BERLIM

    6) Crie um arquivo .txt  

        #!/bin/bash
        echo 1 > /proc/sys/net/ipv4/ip_forward
        iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE
    
    7) Digite *nano firewall.sh* 
       Insira as informações devidas

        #!/bin/bash
        echo 1 > /proc/sys/net/ipv4/ip_forward
        iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE

    8) Execute com

        chmod +x firewall.sh
        ./firewall.sh

        OBS: Este servidor também estará atuando como um roteador!

____________________________________________________________________________________

    DESLIGUE OS SERVIDORES


_____________________________________________________________________________________



    IMPORTAÇÃO DE UMA NOVA MÁQUINA
   
    SRVWEB-DENVER

    1) Crie um grupo no virtualbox

        Botão direito sobre o SRVFW-BERLIM > Criar Grupo
        
        Nome: CENARIO_1

    2) Adicione uma nova placa de rede no SRVFW-BERLIM

        Rede Interna > REDE_SRV

    3) Importe um novo Debian 10.7

        Nome: SRVWEB-DENVER < Desmarque a placa de rede >

    4) configurar o SRVWEB-DENVER

         TELA - 128 MB de memória
              - Controladora gráfica VMSVGA

         ÁUDIO - Desabilite o áudio

        - REDE - ADAPTADOR 2 (Rede interna | REDE_SRV)

       
      

    5) Iniciar o servidor BERLIM - ele que irá fornecer acesso a internet - 
       Iniciar o servidor TÓQUIO - ele fornece conectividade com Putty -
       Iniciar o servidor DENVER - servidor que será acessado

    6) Abra o Putty com o CLIXP-TOQUIO

        Logar com:
         <
            aluno
            Senai@132

            su -
            Senai@132
                       >

    7) Execute o comando ./firewall.sh

__________________________________________________________________________________

    ACESSAR O SRVWEB-DENVER

    1) Logar com:

        root
        Senai@132

    2) Mude o nome da máquina

        hostnamectl set-hostname SRVWEB-DENVER

        OBS: De um LOGOU para mudar o nome

    3) Ver os endereços de IP com

        ip a

    4) Altere o arquivo nano /etc/networks/interface

        ALTERAÇÃO
        # This file describes the network interfaces available in your systemctl
        # and how to activate them. For more information, see interafaces(5).

        source /etc/network/interfaces.d/*

        # The loopback network interface
        auto lo
        auto lo inet loopback

        # The primary network interface
        auto enp0s3
        iface enp0s3 inet static
            address 172.31.0.253
            netmask 255.255.255.0
            gateway 172.31.0.254

    5) Reincie a interface 

          systemctl restart networking.service

    6) Acesse o <CLIXP-TOQUIO>

    7) Insira o comando nano /etc/networks/interface

        Adicione as seguintes características

            # The third network interface
            auto enp0s9
            iface enp0s9 inet static
                address 172.31.0.254
                netmask 255.255.255.0

    8) Suba a interface de rede 

       ifup enp0s9

    9) Veja se a nova placa de rede está ativa
        
       ip a

       *Faça o teste de ping para 172.31.0.253*

    10) No SRVWEB-DENVER

        Testar o ping por IPv4 - funciona
        Testar o ping pelo DNS - falha

        CORREÇÃO
        acesse o arquivo nano /etc/resolv.conf e configure com as informações

            domain localdomain
            search localdomain
            nameserver 8.8.8.8

        Repita o teste de ping pelo DNS

    11) Instale os seguintes pacotes

        apt install vim openssh-server -y
