# PFSENSE INTRODUÇÃO - 16/09

### ORGANIZAÇÃO CENÁRIO

    * Importar uma nova máquina para instalarmos o pfense
        Nome: SRVFW-BERLIM-PFSENSE
        Tipo: BSD
        Tamanha: 20GB (VDI)

    * Configurações
        - Geral > Desativar disquete
        - 32MB de vídeo
        - 1500MB de RAM
        - Selecione um disco rígido "vazio"
            pfSense-CE-2.4.5-RELEASE-p1-amd64
        - Desabilite o áudio
        - Rede
            Adaptador 1 = NAT
            Adaptador 2 = Rede interna (REDE_INTERNA)
            Adaptador 3 = Rede interna (REDE_SRV)

-----------------------------------------

**INSTALAÇÃO - PFSENSE**

    - Deixe a execução acontecer
        Clique em "accept" > OK

    - Opção de teclado = Brazilian (accent keys)
        Continue

    - Configuração de disco = Enter
    
    - Fazer mais coisas (manuais) = não
        Reboot na máquina

    - Remova o disco

-----------------------------------------

**MANUSEIO**

    1) Sequência - Definição IP placa de rede
        2
        2
        10.10.0.6
        29
        enter
        enter
        n
        y
        enter

    2) Sequência - habilitar SSH
        14
        y

-----------------------------------------

**ACESSO SSH e HTTP - PFSENSE**

    1) No CLI7WIN, teste o ping para 10.10.0.6

    2) Abra uma nova sessão no putty para o PFSENSE
        login = admin
        senha = pfsense

    3) No navegador do CLI7WIN. digite 10.10.0.6

        User = admin
        senha = pfsense

        - Next
        - Next

    4) Configurações

        Hostname: SRVFW-PFSENSE
        Domain: projetos.lin.br
        Primary DNS Server: 192.168.1.41
        Second DNS Server: 8.8.8.8
        Time server hostname: 200.160.7.186
        Timezone: America/Sao_paulo
            Next
        Admin Password: Senai@132
            Confirme a senha
        Reload 

        
-----------------------------------------

**DASHBOARD - PFSENSE**

    * "Chave" nos mostra as informações que queremos colocar sobre o template
    * Ícone de "mais", adiciona outros templates

    1) Ligar placa de rede
        Interfaces > Assignments > WAN
            - Save > Apply

        Interfaces > Assignments > LAN
            - Description: REDE_INTERNA
            - Save > Apply

        Interfaces > Assignments > OPT1
            - Enable Interface
            - Description: REDE_SRV
            - IPv4 Configuration Type: Static IPv4
            - IPv4 Address: 172.31.0.254/24
            - Save > Apply

-----------------------------------------

**TESTE**

    1) Ligue o SRVMON-MOSCOU

    2) Sequência - teste de ping (pfsense --> moscou)
        7
        172.31.0.250
        8.8.8.8
        www.uol.com.br

-----------------------------------------

**CRIAÇÃO DE GRUPOS E USUÁRIOS**

    1) Criação de grupos
        System > User Manager > Group

            - Group name: suporte
            - Scope: local
            - Description: Grupo de Técnicos que vão dar suporte
            - Group membership: admin
                Save

    2) Criação de usuários
        System > User Manager > Users

            - Username: suporte1
            - Password: Senai@132
            - Full Name: Lucas Cabral
            - Group membership: admin, suporte
                Save

            - Username: suporte2
            - Password: Senai@132
            - Full Name: Mendes Correa
            - Group membership: admin, suporte
                Save

    3) Alteração das permissões (telas que o usuário poderá utilizar)
        System > User Manager > Users > seu-usuário > Assigned privileges

