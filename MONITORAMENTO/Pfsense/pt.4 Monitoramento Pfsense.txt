VPN - pfSense - Aula 21/09/21

    Configuração do Cenário

        * Importar CLI7WIN-TOQUIO (Nomear para "CLI7WIN-TOQUIO-2")
        > Placa de Rede - Modo bridge

            192.168.5.124/16
            192.168.1.1 - GW
            192.168.1.41 - DNS1
            192.168.1.33-DNS2

    Curiosidade - liberar acesso remoto ao SRVDC-NAIROBI

        Firewall > NAT > Encaminhamento de Portas

        Configuração:

            * Interface: WAN
            * Protocolo: TCP
            * Endereço de origem: *
            * Portas de Origem: *
            * Endereço de Destino: WAN Address
            * Portas de Destino: 3389 (MS RDP)
            * IP NAT: 172.31.0.252
            * Portas NAT: 3389 (MS RDP)
            * Descrição: Acesso ao SRVDC-NAIROBI

------------------------------------------

CLI7WIN-TOQUIO

    * VPN > OpenVPN > Wizards

        Type of Server: Local
        Descriptive name: vpn-senai | ca_vpn_senai
        Key lenght: 2048bit
        Lifetime: 365
        Country Code: BR
        State: SAOPAULO
        City: SAOPAULo
        Organizations: SENAI INFORMATICA

            Interface: WAN
            Protocol: UDP
            Local port: 1194
            Description: vpn_clientes_externos

                Tunnel Network: 20.0.0.0/24
                Redirect Gateway: (selecionado)
                Local Network: 10.0.0.0/24
                Inter-Client Communication: (selecionado)
                DNS Default Domain: 192.168.1.41
                DNS Server 1: 192.168.1.33

                    Firewall Rule: (selecionado)
                    OpenVPN rule: (selecionado)

    * SystemPackage > Manager > Available Packages > Available Packages

        openvpn-client-export > Install > Confirm

            Nota: versão - 2.4.5 DEPRECATED (system > update)

    * Criar um usuário (técnico) e um grupo (acesso_externo)
    
    * Atrelar o certficado ao usuário

            System > User Manager> Users > Edit
                Add (certificate)

            System > Certificate Manager > Certificates > Edit
                365 dias
                commmon name: ac_ext_acesso

            Legacy Windows Installers (2.4.9-Ix01) > 7/8/8

------------------------------------------

APÓS O DOWNLOAD DO ARQUIVO (openvpn-SRVFW-PFSENSE-UDP4-1194-tecnico-install-2.4.9-I601-Win7)

    * Mova o arquivo do CLI7WIN-TOQUIO para a máquina local
    * Após isso, mova o arquivo da máquina local para o CLI7WIN-TOQUIO2
