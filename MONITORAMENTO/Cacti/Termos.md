# TERMOS

**Monitorar = visibilidade - ambiente gerenciado**

    - Manutenção Proativa
    - Manutenção Reativa

    Ferramentas de monitoramento:

        * Dynatrace
        * Nagios
        * JFFNMS
        * MRTG
        * Cacti
        * ZABBIX

**GERENTE -> Administra outros dispositivos**

**AGENTE -> Indivíduo monitorado**

    Comunicação AGENTE <- GERENTE = Puxando

    Comunicação AGENTE -> GERENCIAMENTO = Trap

**SNMP (protocolo de gerenciamento de rede simples) = UDP / 161**

    HOST_A - SO - Memória - CPU - Disco - Consumo de Rede - Usuários logados
    hOST_B - SO - Memória - CPU - Disco - Consumo de Rede - Usuários logados

    Serviço = snmpd (d = daemon | background) = Gerente
              snmp = Agente

    MIB (Management Information Base) = Base de informações 

        * OID = Identificador de Objeto (número único)

    Árvore (modelo hierárquico)

        * Padrão ISO

    Comando - exemplo

        * snmpwalk -c SALA02 -v 2c 192.168.132.100 | mais

    SNMP VULNERABILIDADES

        * SNMP está em uma comunidade "pública"! As botas podem roubar e alterar as informações de TODO o ambiente
