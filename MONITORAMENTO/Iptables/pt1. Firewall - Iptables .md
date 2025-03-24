# Introdução IPtables

 > **DEFINIÇÃO**

        <> Firewall é uma solução de segurança baseada em um conjunto de regras ou instruções. 
      (Analisa o tráfego de rede para determinar quais operações de transmissão ou recepção de dados podem ser executadas.)

        <> "Parede de fogo" (tradução literal do nome).

        <> Objetivo: bloqueio de tráfego de dados indesejados e liberação de acesso bem-vindo.

 ### TIPOS DE FIREWALL

        <> Filtragem de pacotes | Funciona até a camada 4

        <> Firewall de aplicação ou proxy de serviços | Funciona até a camada 7

  **Filtragem de pacotes** 

            * Firewall que toma decisões baseadas nos parâmetros do pacote: porta, endereço de origem / destino, estado da 
            conexão..
            * O firewall pode negar o pacote (DROP) ou deixa-lo passar (ACEPPT).

  **Firewall de Aplicação ou Proxy de Serviços (Proxy Services)**

            * Firewall que analisa o conteúdo do pacote para tomar suas decisões de filtragem.
            * Firewall do tipo intrusivo - analisa todo o conteúdo que passar e permite um controle relacionado 
            com o conteúdo do tráfego.

### IPTABLES

    <> Funciona por meio da comparação de regras.

    <> Firewalls restritivos - o pacote é bloqueado e registrado ao administrador do sistema.

   **SINTAXE**
  
        iptables [-t tabela] [opção] [cadeia] [dados] -j [ação]
        aplicativo> tabela> opção> mecanismo> condicional> ação

### TABELA

   **FILTER**
   
  *Tabela padrão, usada no tráfego de dados comum.* 

          ! Contém 3 chains padrões:
     
                  --> INPUT consultada para dados que chegam ao servidor;
                  --> OUTPUT consultada para dados que saem do servidor;
                  --> FORWARD consultada para dados que são redirecionados
                  para outra interface de rede ou outra máquina.


   **NAT**
   
   *Usada para concentrar o fluxo de varias conexões, saindo para
    uma única.* 
   
           ! Contém 3 chains padrões:

                 --> PREROUTING Consultada quando os pacotes precisam ser
                 modificados logo que chegam ao firewall. É a chain ideal para
                 realização de DNAT e redirecionamento de portas;

                 --> OUTPUT Consultada quando os pacotes gerados
                 localmente precisam ser modificados antes de serem
                 roteados. Esta chain somente é consultada para conexões
                 que se originam de IP’s de interfaces locais;

                 --> POSTROUTING Consultada quando os pacotes precisam
                 ser modificados após o tratamento de roteamento. É a chain
                 ideal para realização de SNAT e IP Masquerading

  **MANGLE**
  
  *Utilizada para alterações especiais de pacotes (como modificar o
   tipo de serviço (TOS).*
   

		 --> INPUT entrada.
		 --> FORWARD repasse.
		 --> PREROUTING Consultada quando os pacotes precisam ser
		     modificados logo que chegam.

  
     Parâmetros
              - P Policy (Define uma regra
		  - N New (Criar nova Chain)
              - E Rename (Renomeia a Chain Criada por N)
	          - F Flush (Apaga todas as Regras)
		  - X eXtract (Limpar Chain Criada por N)
	          - Z Zero (Zerar Regras específicas)

                                                      

      POLÍTICA

          Firewall Permissiva -> Liberar tudo para depois bloquear (Exemplo: Linux)
          Firewall Restritiva -> Bloquear tudo para depois liberar (Exemplo: Windows)

            * Mandatória
            * Regra -> Está dentro da política
