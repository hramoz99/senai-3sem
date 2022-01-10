CENÁRIO


 * Criação de um arquivo de script para o firewall - Local para adicionar as declarações de políticas e regras
	#touch firewall
	
 * Tornar o arquivo executável
	#chmod + x firewall

 * Dentro do arquivo adicione uma sintaxe de script
	#! / bin / bash
	
 * Testar o "botão" do script
	#. / firewall

 * Tornar o firewall inicializável junto ao sistema operacional
	
     Criar arquivo no caminho
           #vim /etc/systemd/system/firewall.service

	Inserir no arquivo
		[Unidade]
		Descrição = Firewall

		[Serviço]
		Tipo = bifurcação
		ExecStart = / etc / init.d / firewall start

		[Instalar]
		WantedBy = multi-user.target
		
	Mover o arquivo "firewall" para o novo caminho
		#mv / root / firewall /etc/init.d/

	Editar o arquivo "firewall" 
         ! Adicionar uma instrução de nível de execução 
		#! / bin / bash
		### BEGIN INIT INFO
		# Início padrão: 2 3 4 5
		### END INIT INFO
		
	Habilitar para inicialização automática
		#systemctl enable firewall.service
		
 COMANDOS 
 ! Listar conteúdo da tabela filter
	iptables -L
	
 ! Listar conteúdo da tabela filter sem resolução de nome (n) e apresentar a linha de cada regra em sua cadeia (--line-numbers)
	iptables -L -nv --line-numbers
	
 ! Deletar a regra da linha 2 da cadeia INPUT
	iptables -D INPUT 2