# MONITORAMENTO COM CACTI (17/08) 

______________________________________

**NAIROBI**

    1) Clieque em 'Gerenciador de servidor'> Recursos> Adicionar recursos> Marque "Serviços SNMP"> Avançar> Instalar

    2)  Configuração> Serviços> Serviços SNMP> clique 2x> Parar

     **Características**

            AGENTE

                * Administrador.admin@projetos.win.br  <Contato>
                * São Paulo - Matriz <Localização>

            ARMADILHAS
            
                * Público> Adicionar> 172.31.0.251 (IP)

            SEGURANÇA

                * Comunidade: pública <SOMENTE LEITURA>
                * Aceitar pacotes SNMP dos hosts > Adicionar > 172.31.0.251

---------------------------------------
**FIREWALL - REGRA DE ENTRADA**

    Firewall do Windows > Segurança Avançada > Funções de Entrada

        Tipo de função = porta
        Protocolo e portas = UDP - 161 <portas locais específicas>
        Ação = Permitir a conexão
        Perfil = Domínio, Privado e Público
        Nome = SNMP-Libera-161

---------------------------------------
**TÓQUIO**

    3) Criar um novo dispositivo no Cacti 

        * Descrição: SRVDC-NAIROBI
        * Nome do host: 172.31.0.252
        * SNMP genérico

        OBS: Em caso de erro, desabilite o firewall do windows

---------------------------------------

    !Configurações na máquina Berlim e Denver.

---------------------------------------

**BERLIM**

    1) 'apt update -y'
    2) Atualização do apt -y
    3) 'apt install snmp snmpd -y'
    4) vim ou nano /etc/snmo/snmpd.conf 
        *Alterar a linha 15 <udp: 161>
        *Alterar a linha 51 <apague até o 0 '-V'>
        *Alterar syslocation <nome_do_servidor> e syscontact <Admin <admin@projetos.lin.br>

    5) 'systemctl restart snmpd.service'

    Dispositivo: Crie um Novo (Core)
    IP: 172.31.0.254

    Local: novo gráfico (Disk Bytes)

---------------------------------------

**DENVER**

    1) 'apt update -y'
    2) Atualização do apt -y
    3) 'apt install snmp snmpd -y'
    4) vi /etc/snmo/snmpd.conf 
        *Alterar a linha 15 <udp: 161>
        *Alterar a linha 51 <apague até o 0 '-V'>
        *Alterar syslocation <nome_do_servidor> e syscontact <Admin <admin@projetos.lin.br>

    5) systemctl restart snmpd.service

    Dispositivo: Crie um Novo (Core)
    IP: 172.31.0.253
