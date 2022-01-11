# ROTEIRO

 *"O troubleshooting pode ser compreendido como uma espécie de diagrama de ações, um conjunto de medidas que orienta a resolução de problemas dentro do ambiente de TI.
  Em tradução, troubleshooting significa solução de problemas.”*

**PROBLEMA**: *“ Um funcionário, ao ser demitido, danificou a infraestrutura funcional da empresa, deixando-a fora do ar. 
Você e sua equipe, sendo chamados como consultores para resolverem os problemas, deverão colocar este mesmo ambiente no ar novamente.
Assim, auxiliando na diminuição do prejuízo desta empresa que os contrataram.”*


#### CONFIGURAÇÃO DA REDE
 

	- Realizar a cópia (backup) de todo arquivo de configuração
	- Estado dos serviços que serão analisados
	- LOG de Sistema

#### CENÁRIO - PREPARAÇÃO DO AMBIENTE
MODELO OSI - 7 CAMADAS

	7 - APLICAÇÃO - Navegador / Apache2 / FTP

	6 - APRESENTAÇÃO - Codificação

	5 - SESSÃO - Autenticação

	4 - TRANSPORTE - TCP/UDP/ICMP | Divisão da parte física para a parte lógica do serviço

	3 - REDE (NET) - ROTEADOR (DOMÍNIO DE 	BROADCAST) | Conectar redes diferentes | Segmentação

	2 - ENLACE (LINK LAYER/FRAME) | Enquadramento da informação | Organização de termos binários (com começo, meio e fim) - SWITCH (DOMÍNIO DE COLISÃO)

	1 - FÍSICA | Wireless, Cabo | Energia elétrica convertida em 0s e 1s (binário) - HUB (REPETIDOR) / CONECTORIZAÇÕES

FÍSICO (Virtualização - VirtualBox)

	* Import das máquinas virtuais
	* Configuração das interfaces de rede (NIC)
	* Conexões de Switch

LÓGICO (Sistema operacional)

	 CONFIGURAÇÃO BASE
		 Hostname
		 Interface(s) de rede
		 Usuário/Grupos

	 SERVIÇOS
		 Acesso Remoto
		 Roteamento/NAT
		 DNS
		 WEB
		 DHCP

#### SRVLNX-NAIROBI

FÍSICO (Virtualização - VirtualBox)
        
	
	Import das máquinas virtuais
        Configuração das interfaces de rede (NIC)
                A1 - NAT
                A2 - Rede interna: LAN Segment
        Conexões de Switch
                LAN Segment
				
		
LÓGICO (Sistema operacional)


        Configuração base
                Hostname:
                        SRVLNX-NAIROBI
                Interface(s) de rede
                        A2(REDE INTERNA) enp0s8 - 
                                Address: 172.31.100.253
                                Netmask: 255.255.255.0
                        A1(NAT) - enp0s17
                                DHCP
                                #"editor" /etc/network/interfaces
                Usuário/Grupos
                        #cat /etc/passwd
                Outra*
        
        SERVIÇOS
                ACESSO REMOTO (openssh-server)
                        Não existia instalação!
                ROTEAMENTO/NAT
                DNS (bind9)
                        #Arquivo com o Resolver (DNS para consulta pelo equipamento em questﾃ｣o)
                        /etc/resolv.conf
                        #Arquivo de declaração das zonas
                        /etc/bind/named.conf.local
                        #Arquivo de entrada da zona direta nairobi00.com.br
                        /etc/bind/db.nairobi00.com.br
                        #Arquivo de entrada da zona reverso nairobi00.com.br
                        /etc/bind/db.reverso.nairobi00.com.br
                        #Configurar seguindo a boa prática
                        /etc/bind/named.conf.options
                
                        Cópia dos arquivos acima para o diretório /root/bkp/bind
                        
                        
                        
                WEB (apache2)
                        #Armazenamento da página existente
                        /var/www/site                        
                        #Arquivos de configuração do Apache2
                        #Páginas disponíveis
                        /etc/apache2/sites-available
                        #Páginas disponﾃｭveis - Site.conf
                        /etc/apache2/sites-available/site.conf
                        #Páginas ativas
                        /etc/apache2/sites-enabled
                        #Verificar a porta de funcionamento do serviço HTTP
                        /etc/apache2/ports.conf
                        


#### SRVWIN-RIO
FÍSICO (Virtualização - VirtualBox)



        Import das máquinas virtuais
        Configuração das interfaces de rede (NIC)
                A1 - LAN Segment
        Conexões de Switch
                LAN Segment
                
LÓGICO (Sistema operacional)

        CONFIGURAÇÃO BASE
                Hostname
                        SRVWIN-RIO
                Interface(s) de rede
                Usuário/Grupos
                Outra*
        
        SERVIÇOS
                Acesso Remoto
                DHCP
                        Dynamic Host Configuration Protocol
                                REDE
                                Máscara
                                Gateway
                                Escopo(Range)
                
#### CLTWIN-OSLO                
FÍSICO (Virtualização - VirtualBox)


        Import das máquinas virtuais
        Configuração das interfaces de rede (NIC)
                A1 - LAN Segment
        Conexões de Switch
                LAN Segment
                
LÓGICO (Sistema operacional)

        CONFIGURAÇÃO BASE
                Hostname
                        sysdm.cpl
                                CLTWIN-OSLO
                Interface(s) de rede
                        DHCP
                Usuário/Grupos
                        lusrmgr.msc
                Outra*
        
        SERVIÇOS
                Acesso Remoto




Caminhos importantes:
/etc/network/interfaces
