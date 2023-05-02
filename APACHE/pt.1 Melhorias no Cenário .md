# OTIMIZAÇÃO DO CENÁRIO 1 

 **SRVFW-BERLIM**

 * Instalar openssh & vim
 * Acessar 'vim /etc/network/interfaces'

        Alterar o IP para 10.10.0.6
        Máscara: 255.255.255.248

    <>  Reiniciar as configurações de rede:

            systemctl restart networking.service

    <> Verificar o acesso SSH está ativo

            systemctl status ssh.service

-----------------------------------------------

 **ACESSO - WINXP**

    1) Adicionar um novo disco (Virtualbox)

    2) Alterar as configurações de rede
          <
            IP: 10.10.0.1
            MASK: 255.255.255.248
            GW: 10.10.0.6
                          >
            *Teste de ping com GW*

  >  NOTA: O ping para a internet falhará. 
   
   **ALTERAR CONFIGURAÇÃO**

    3) Alterar as informações para bi-direcional [Arraste para a Área de trabalho compartilhada]

-----------------------------------------------

**ACESSO - SRVFW-TOQUIO**

    1) Digitar o comando
          echo 1 > /proc/sys/net/ipv4/ip_forward

    2) Digitar o comado    
          iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE

-----------------------------------------------

**ACESSO - WINXP**


    1) Teste de ping - DNS do google

    2) Baixar o Putty (32bit)

          https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html

    3) Acessar a máquina virtual pelo putty

        Name: SRVFW-BERLIM
        IP: 10.10.0.6

              User: aluno
              Senha: Senai@132

___________________________________________________________________

   **EM CASOS DE PROBLEMAS**

        ! Verificar se o usuário existe
                 cat /etc/passwd | grep aluno


        *! Modificar a senha do usuário (opcional)

               passwd aluno

                 Nova senha:
                 Redigite a nova senha:

    4) Logar com o usuáio root

        su -
        Senha: Senai@132

    5) Alterar o nome do servidor 
         hostnamectl set-hostname [nome]

    6) Criar arquivo.txt  

        #!/bin/bash
        echo 1 > /proc/sys/net/ipv4/ip_forward
        iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE
    
    7) Digitar *nano firewall.sh* 
       Insira as informações

        #!/bin/bash
        echo 1 > /proc/sys/net/ipv4/ip_forward
        iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE

    8) Executar 

        chmod +x firewall.sh
        ./firewall.sh

        OBS: Este servidor também estará atuando como um roteador!

____________________________________________________________________________________

**IMPORTAÇÃO DE UMA NOVA MÁQUINA**
   
  **SRVWEB-DENVER**


    1) Adicionar uma nova placa de rede na máquina virtual

        Rede Interna > REDE_SRV

    2) Importe um novo Debian 10.7

        Nome: SRVWEB-DENVER < Desmarque a placa de rede >

    3) configurar a outra MV

         TELA - 128 MB de memória
              - Controladora gráfica VMSVGA

         ÁUDIO - Desabilitar

        - REDE - ADAPTADOR 2 (Rede interna | REDE_SRV)


 *Servidor BERLIM - fornece acesso a internet*
 
 *Servidor TÓQUIO - fornece conectividade com Putty*
 
 *Servidor DENVER - host acessado*

    4) Abrir o Putty com o CLIXP-TÓQUIO

        Logar com:
         <
            aluno
            Senai@132

            su -
            Senai@132
                       >

    5) Executar o comando ./firewall.sh

__________________________________________________________________________________

**ACESSO - SRVWEB-DENVER**

    1) Logar com:

        root
        Senai@132

    2) Configurar o nome da máquina

        hostnamectl set-hostname SRVWEB-DENVER

        OBS: De um LOGOU para mudar o nome

    3) Verificar os endereços de IP com
        ip a

    4) Alterar o arquivo 'nano /etc/networks/interface'

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

    5) Reinciar a interface 
          systemctl restart networking.service

    6) Acessar <CLIXP-TOQUIO>

    7) Insirir o comando 'nano /etc/networks/interface'

        Adicionar características

            # The third network interface
            auto enp0s9
            iface enp0s9 inet static
                address 172.31.0.254
                netmask 255.255.255.0

    8) Conectar a interface de rede 
       ifup enp0s9

       ! Faça o teste de ping para 172.31.0.253*

    9) SRVWEB-DENVER

        Testar o ping por IPv4 - on
        Testar o ping pelo DNS - off

      ! CORREÇÃO
        acessar o arquivo 'nano /etc/resolv.conf e configure as informações'

            domain localdomain
            search localdomain
            nameserver 8.8.8.8

    10) Instalar os pacotes
        apt install vim openssh-server -y
