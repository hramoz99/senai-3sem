# PfSense - Aula 23-09-21
_________________________________________________

**CLI7WIN2-TÓQUIO**

     Baixar o arquivo https://swupdate.openvpn.org/community/releases/tap-windows-9.21.2.exe


**CLI7WIN-TÓQUIO**

           Apagar os certificados e as regras de segurança relacionadas a VPN (OpenVPN)
          (Por questões de organização, apague o usuário e o certificado atrelado a ele)

      * Criar uma nova VPN
        VPN > OpenVPN > Wizards

        <> Create a New Certificate Authority (CA) Certificate
            Descriptive name: vpn_manha
            Key length: 2048bit
            Lifetime: 365
            Country Code: BR
            State: SAOPAULO
            City: SAOPAULo
            Organizations: SENAI

                <> Create a New Server Certificate
                    Descriptive name: vpn_manha
                    Key length: 2048bit
                    Lifetime: 365
                    Country Code: BR
                    State: SAOPAULO
                    City: SAOPAULo
                    Organizations: SENAI

                        <> General OpenVPN Server Information
                            Interface: WAN
                            Protocol: UDP on IPv4 only
                            Local port: 1194
                            Description: vpn_manha
                            - TLS Authentication
                            - Generate TLS Key
                            DH Parameters Length: 2048
                            Encryption Algorithm: AES-128-GCM
                            Tunnel Network: Tunnel Network
                            Local Network: 172.31.0.0/24
                            - Inter-Client Communication
                            - Duplicate Connections
                            - Dynamic IP
                            - Firewall Rule
                            - OpenVPN rule

       * Criar um usuário
           System > User Manager > Users

            <> Edit
                Username: manha
                Password: Senai@132
                Full name: manha

                    <> Create Certificate for User
                        Descriptive name: vpn_aluno_manha
                        Certificate authority: vpn_manha
                        Key length: 2048bit
                        Lifetime: 365

    * Baixar o cliente VPN
            OpenVPN > Client Export > OpenVPN Clients

                <> Export
                    Legacy Windows Installers (2.4.9-Ix01): openvpn-SRVFW-PFSENSE-UDP4-1194-manha-install-2.4.9-I601-Win7

    

----------------------------------------------------

**CLI7WIN2-TÓQUIO**

    * Execute o arquivo 'openvpn-SRVFW-PFSENSE-UDP4-1194-manha-install-2.4.9-I601-Win7'
        Siga o fluxo natural da instalação

    * Execute o arquivo 'tap-windows-9.21.2'
        
    * Clique em Iniciar > TAP-Windows > Utilities > Add a new TAP virtual ethernet

            <> OpenVPN GUI
                Conectar 
                - User:
                - Senha:

    * Novo adaptador aparecerá nas Conexões de Rede

    * Essa informação pode ser visualizada em
        
        <> cmd > ipconfig

        <> pfsense
            Status > OpenVPN

    * Windows + R > cmd (entre como administrador)

        <> ipconfig
            route -p add 172.31.0.0 mask 255.255.255.0 10.20.100.2 if 4
            route print
            ping 172.31.0.254
            ping 172.31.0.251

    * Acesse o cacti (SRVMON-HELSINQUE) pelo navegador
        172.31.0.251/cacti

----------------------------------------------------

**COMPARTILHAMENTO DISCO**

    * Windows Explorer - SRVDC-NAIROBI

        <> Clique com o botão direito sobre o disco > Properties > Sharing > Marque a opção 'Share the folder'
        - Share Name: D (por exemplo)
        - Permissions: Everyone > Allow

    * Windows Explorer - CLI7WIN2-TOQUIO

        <> Clique com o botão direito sobre 'Computador' > Mapear unidade de rede 
        - Unidade: D (por exemplo)
        - Pasta: \\172.31.0.252\d
            Concluir

                <> Login
                - User: projetos\Administrator
                - Senha: [senha-do-srvdc-nairobi]
