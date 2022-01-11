# FIREWALL - ASA (CISCO) - 13/09

    ASDM - Interface gráfica (via web) para configuração do ASA

#### TIPOS DE FIREWALL
```
    - IPtables > ferramenta da linha de comando (Linux)
    - Windows > firewall do Windows, norton, AVG, Macaffe
```

#### CISCO ASA - LÓGICA

    - Regras de entrada
    - Regras de saída
    - Regras para encaminhamento

     * Porta para gerenciamento (via rede) = Management 1/1
     * Porta console = fisicamente conectado

--------------------------------

#### OBSERVAÇÕES 
```
    * Senha de primeiro acesso no terminal - não existe (apenas aperte 'enter')
    * Ao utilizar classe cheia (A, B ou C) para a distribuição dos IPs, não é obrigatório colocar a máscara
    * Comando 'sh run' funciona em qualquer modo/menu da console
    * ASA - por padrão possui a política de modo "DROP" -> no security-level
        ! Necessário a definição de um nome e um nível para cada segurança

   INSEGURO = 0 (internet)
    .
    .
    .
   SEGURO = 100 (local/LAN)

    * Níveis mais altos --> níveis mais baixos (OK)
    * Níveis mais baixos --> níveis mais altos (Falha)
        ! Obrigatoriedade do uso de ACLs

   PACKET TRACER - permite conexão ssh
        ! Clicar no PC ou laptop e rolar até 'Telnet / SSH Client'

    * Timeout máximo do ssh - 60 segundos

    * Visualizar todas as listas disponíveis
        1) sh access-list
        - hintcnt = quantas vezes essa regra foi utilizada

        * Visualização da regra e da interface que a foi aplicada
        2) sh run | include access
        - Esse parâmetro funcionará apenas se as ACLs existirem

    * Interface nomeada em "outside" = mais inseguro
        ! Automaticamente o ASA entende que o security-level dessa interface é igual à zero (0)

    * Interface nomeada em "inside" = mais seguro
        ! Automaticamente o ASA entende que o security-level dessa interface é igual à cem (100)

    * Comando 'sh int ip brief'
        Apresenta os IPs atrelados a cada interface
```        
        
# CENÁRIO

  *IP dos PCs -> segundo IP válido*

  *Script - CISCO ASA*

#### CONFIGURAÇÃO DAS INTERFACES 
```
en
conf t 
int g1/1
nameif a
ip add 192.168.10.1
no sh
int g1/2
nameif b
ip add 192.168.20.1
no sh
int g1/3
nameif c
ip add 192.168.1.1
no sh
```

#### DEFINIÇÃO DOS NÍVEIS DE SEGURANÇA DAS INTERFACES - TESTE DE PING 
```
int g1/1
security-level 0
int g1/2
security-level 0
int g1/3
security-level 0
```

#### DEFINIR ZONA INTERMEDIÁRIA - 'DMZ' (ATRIBUIR CAMADA DE SEGURANÇA)
```
int g1/1
security-level 0
int g1/2
security-level 50
int g1/3
security-level 100
```

#### LIGAR PLACA DE REDE - GERENCIAMENTO 
```
interface management 1/1
nameif gerencia
security-level 0
ip add 172.16.0.1
no sh
```

#### CRIAÇÃO DO ACESSO SSH 
```
username admin password Senai@132
ssh 172.16.0.0 255.255.0.0 gerencia
aaa authentication ssh console LOCAL
ssh timeout 60
```

#### PERMITIR PING DA INTERNET PARA DMZ 
```
access-list T1 extend permit icmp host 192.168.10.2 host 192.168.20.2
access-group T1 in interface a

# Permitir ping da Internet para LOCAL-LAN
access-list T1 extend permit icmp host 192.168.10.2 host 192.168.1.2

# Apagar as regras - Liberação icmp para toda a rede
no access-list T1 extend permit icmp host 192.168.10.2 host 192.168.20.2
no access-list T1 extend permit icmp host 192.168.10.2 host 192.168.1.2
#
access-list T1 extend permit icmp any any
access-group T1 in interface a
access-group T1 in interface b
```

#### SALVAR AS CONFIGURAÇÕES 
```
write memory
```
