# MONITORAMENTO COM ZABBIX - (19/08)

 **INSTALAÇÃO DO SERVIDOR DE MONITORAMENTO**


----------------------------------------------------------------------------


### PREMISSAS TÉCNICAS
    Rede: 172.31.0.0/24


**VIRTUALIZADOR - VirtualBox**

    Importação da máquina virtual: 'Debian 10.7 Base.ova'
    Configuração das Interfaces de Rede: 'Adaptador 1 - Rede Interna Rede_SRV'
           

**SISTEMA OPERACIONAL**
```
     Nome: SRVMON-MOSCOU
            #hostnamectl set-hostname SRMON-MOSCOU
            #bash
```

**INTERFACE DE REDE**

        #ip a
        # vim.tiny / etc / network / interfaces

         enp0s3 
             auto enp0s3
             iface enp0s3 inet static
             endereço 172.31.0.250
             máscara de rede 255.255.255.0
             gateway 172.31.0.254

**RESTART DO SERVIÇO**

            # / etc / init.d / networking restart
            #service networking restart
            #systemctl restart networking.service


**Verificação do GATEWAY**

      #ip route


**Teste de Cominicação**

         ping para o gateway
            
         ping para a internet

        DNS - RESOLVER
        ! APONTAR PARA OS SERVIDORES DO CENÁRIO
            nameserver 172.31.0.253
            servidor de nomes 172.31.0.252

        TESTE DO DNS RESOLVER
              ping / nslookup 

    Configurações Básicas - Atualizar as listas de pacotes
                            #apt update

                            Atualizar a distribuição
                            #apt upgrade

        VIM 
            #apt install vim
                Editar o programa
                    #vim / etc / vim / vimrc
                        Linha 26 - descomentar
                        Linha 27 - criar um conjunto de números

        SSH (servidor openssh)
            #apt install openssh-server
                Editar as configurações de acesso SSH para ativar a permissão do ROOT
                    #vim / etc / ssh / sshd_config
                        Linha 32 - descomentar e alterar
                                   
                           PermitRootLogin sim

**Serviços Específicos**
        
    Adicionar Interface Secundária - Comunicação com o Windows
    VirtualBox - ativar adaptador2
            
    Placa de rede - Exclusiva de hospedeiro (somente host)

        Inteface Linux
            # vim / etc / network / interfaces
                
              enp0s8
                    auto enp0s8
                    iface enp0s8 dhcp
                    
         ZABBIX
            zabbix.org
