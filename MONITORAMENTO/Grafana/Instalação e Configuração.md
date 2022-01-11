INSTALAÇÃO E CONFIGURAÇÃO (26/08)

GRAFANA produz gráficos por meio da base de dados fornecidos pelas ferramentas de monitoramento
       .Zabbix
       .Cacti

INSTALAÇÃO GRAFANA

    1) wget -q -O - https://packages.grafana.com/gpg.key | apt-key add -
    2) echo "deb https://packages.grafana.com/oss/deb stable main" | tee -a /etc/apt/sources.list.d/grafana.list
    3) Atualizar os pacotes
        atualização apt
        atualização apt
    4) apt install grafana -y
    5) systemctl daemon-reload
    6) systemctl enable grafana-server
    7) systemctl start grafana-server
        systemctl status grafana-server
    8) ss -ntpl | grep grafana (usa porta 3000)
    9) plug-ins grafana-cli instalam alexanderzobnin-zabbix-app
    10) systemctl reiniciar grafana-server

---------------------------------------------------------------------

GRAFANA

    1) Configurações > Plug-ins> Zabbix> Habilitar
    2) Configurações> Fonte de dados> Adicionar fonte de dados> Zabbix
        
    Definições
            URL: http://172.31.0.250/zabbix/api_jsonrpc.php
            Nome de usuário: Admin
            Senha: zabbix
        !Salvar -> "Zabbix API versão 5.0.14"
    3) Logout no Grafana -> Botão de ajuda> Sair

----------------------------------------------------------------------

PAINEL 

    1) +> Criar> PAINEL
       Salvar e definir o NOME

    2) Adicionar painel> adicionar painel (vazio)

    3) Consulta

        * Zabbix
        * Métricas
        * Servidores Zabbix 
        * Sistema de arquivos /  Espaço total

    4) Série Temporal> Gráfico de pizza

        Opções Padrão
            Unidade -> Dados / bytes (SI)

    5) Consulta Duplicada
        Espaço total (A) e Espaço utilizado (B)
            Sistema de arquivos / -> espaço utilizado

    6) Salvar> Salvar painel> Espaço em disco> Aply


