# FIREWALL - ASA (CISCO) - 15/09

  *PADRÃO DE CONEXÃO - CISCO*

    Putty > Connection > SSH > Serial


-------------------------------------------------

### PARÂMETROS

    *  User mode - (>)
    * 'Admin' Cisco - modo privilegiado (#)

    - ? (listagem dos comandos disponíveis)
    
    - show version (Versão do Equipamento)
        Ext: Management1/1 = porta de gerenciamento
        Licensed features for this platform = informações de licença
        Configuration has not been modified since last system restart = alterações feitas no sistema
    
    - sh run = mostra as configurações do equipamento

    - sh flash
        asdm-761.bin = arquivo necessário para a executação da interface gráfica

    - sh int ip brief = informações das interfaces e seus IPs

-------------------------------------------------

### HABILITAR INTERFACE GRÁFICA - EXEMPLO

     1) Informar o caminho do sistema gráfico - ASDM
     2) Habilitar o servidor HTTP do ASA
     3) Permitir qual rede terá o acesso ao serviço HTTP

    Nota: O dispositivo de gerenciamento do equipamento deve estar na mesma rede do firewall
        OBS: comando (no cmd) -> 'arp -a', mostra os IPs e seus endereços MAC

#### CONFIGURAÇÃO BÁSICA 
```
en
conf t
int g1/1
ip add 10.10.0.6 255.255.255.248
nameif inside
no sh
```

#### INFORMAR O CAMINHO DO SISTEMA GRÁFICO - ASDM 
```
asdm image flash:/asdm-761.bin
```
#### HABILITAR O SERVIDOR HTTP - ASA 
```
http server enable
```
#### PERMITIR QUAL REDE TEM ACESSO AO SERVIDOR HTTP
```
http 10.10.0.0 255.255.255.248 inside
```
-------------------------------------------------

### TESTE

    No navegador digite http://10.10.0.6

-------------------------------------------------

### INSTALAÇÃO

  *Nota: Depois de acessar a URL na etapa anterior - TESTE*

    1) Clique em'entrar' - Não existe usuário e admin
    2) Install ASDM Laucher (arquivo de 700KB)
    3) Instale o ASDM Launcher
    4) 'Caminho' C:\Program FIles (x86)\Cisco Systems\ASDM
    5) Envie o arquivo asdm-launcher.jar para a área de trabalho (atalho)

-------------------------------------------------

### Cisco ASDM-IDM Launcher

    IP: 10.10.0.6 > OK

-------------------------------------------------

### INTERFACE GRÁFICA

  *Após as alterações na interface gráfica deve-se aplicar (apply) as configurações e salvá-las (save) para que sejam 
  aplicadas na linha de comando do ASA.*

  
