 # MONTAGEM DO CENÁRIO 

 > Importação de duas MV Linux 10 

  **CONCEITOS ESTUDADOS**

   * Operação de máquinas virtuais
   * Operação de interfaces de redes virtuais
   * Acesso à Internet
   *  Grupos e Usuários
 _______________________________________________

### PASSO A PASSO

 1. Importar uma imagem de Máquina no virtualbox
 
          Arquivo > Importar > PASTA DA ISO > Debian 10.7 Base.ova

   > Clique em PRÓXIMO

 2. Alterar o nome da máquina
   EX: SRVFW-BERLIM

 
 3. 'Desmarcar a opção de placa de rede'

   > Clique em IMPORTAR
_____________________________________________	     


**CONFIGURAÇÃO DAS VMs**

      1) Modifique as Especificações de tela

         TELA - 128 MB de memória
              - Controladora gráfica VMSVGA

         ÁUDIO - Desabilitar

        - REDE  ADAPTADOR 1 (NAT)
                ADAPTADOR 2 (Rede interna | REDE_INTERNA)
 
**ACESSO**

    User: *****
    Senha: ****

**TERMINAL**

    1) Visualizar as placas de rede 'ip a'


    2) Editar as informações de rede (IPs)

         Acessar nano /etc/network/interfaces

            # This file describes the network interfaces available in your systemctl
            # and how to activate them. For more information, see interafaces(5).

            source /etc/network/interfaces.d/*

                   # The loopback network interface
                     auto lo
                     auto lo inet loopback

                   # The primary network interface
                     auto enp0s3
                     iface enp0s3 inet dhcp

                   # The second network interface
                     auto enp0s8
                     iface enp0s8 inet static
                     address 172.31.0.254
                     network 255.255.255.0

        - Salvar o Arquivo
        - Ver as configurações novas
   
              cat /etc/network/interfaces

    3) Reiniciar os serviços de rede
           
              systemctl restart networking.service'

       ! Verificar status do servidor 
             *systemctl status networking.services

    4) Digite o comando 'ip a'

       ! Teste de conexão: "apt update"

    5) Atualizar os pacotes
                    apt update -y
 
    6) Alterar o nome da máquina 
                  hostnamectl set-hostname SRVFW-BERLIM

    7) Compartilhar o acesso a internet com toda rede interna

        <> INSTALE

            apt install vim
            apt install openssh-server -y

        <> VERIFIQUE OS STATUS

            systemctl status ssh.service

----------------------------------------------------------------------------------

### IMPORTA UMA NOVA VM - WXPProSP3

  1) Modificar as Especificações de tela

         TELA - 128 MB de memória
              - Controladora gráfica VMSVGA

         ÁUDIO - Desabilite o áudio

        * REDE  ADAPTADOR 1 (NAT)
        
                ADAPTADOR 2 (Rede interna | REDE_INTERNA)


    2) Logar no Servidor (Senha: Senai@132)

    3) Alterar as configurações da placa de rede com

        Windows + R > ncpa.cpl

        Parâmetros

            - IP: 172.31.0.251
            - Máscara: 255.255.255.0
            - GW: 172.31.0.254

            DNS: 8.8.8.8

    4) Adicionar um novo disco óptico no Servidor

        - Desligar a máquina
               <> Configurações > Armazenamento > Adicionar novo disco óptico > Deixar vazio

    5) Ao inicializar a máquina mudar de modo escalonado para modo normal

        Clique em Dispositivo > Inserir imagem de CD...

    6) Acesse 'My Computer' < WinXP >

        Clique em "VirtualBox Guest Additions"

        - Siga a instalação normalmente ('next')
        - Confirme a opção de reboot



 


