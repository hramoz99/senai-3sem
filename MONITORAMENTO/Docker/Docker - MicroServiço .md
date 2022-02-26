# MICROSERVIÇO - 24/09/21

### `CENÁRIO`

     Serviço Necessário -> Conteinerização -- Docker
    
-----------------------------------------------------------------------------

**DEBIAN 10 VM** 

     Alterar a placa de rede
        
          nano /etc/network/interfaces

            <> The primary network interface
            auto enp0s?
            iface enp0s? inet static
                address 192.168.100.1xx
                netmask 255.255.255.0
                gateway 192.168.1.1
        
           'systemctl restart networking.service'

     Alterar o nameserver
       echo 'nameserver 4.2.2.2' > /etc/resolv.conf

     Instalar o SSH
      'apt install openssh-server'

     Atualizar o Debian
      'apt update'

     Aplicar as atualizações
       'apt upgrade'

-----------------------------------------------------------------------------

**DOCKER**

    <> Passo a Passo 
         instalação - https://docs.docker.com/engine/install/debian/

         hostnamectl set-hostname DOCKER
        
         bash
        
       'apt-get install \
        apt-transport-https \
        ca-certificates \
        curl \
        gnupg \
        lsb-release'

        'curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg'

        ! echo \
        "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian \
        $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null

        'apt-get update'

        'apt-get install docker-ce docker-ce-cli containerd.io'

    <> Manipulação

        ! docker run hello-world

        ! docker run -d debian

        ! docker images

        ! docker run -it ubuntu bash
            docker ps
            docker ps -a

            exit (sair)

        ! docker container (apaga o container) prune 

        ! docker rmi (apagar a imagem) hello-world 

        ! docker rmi ubuntu

        ! touch dockerfile
            cat dockerfile
                FROM debian:8.11
                RUN apt-get update && apt-get install apache2 -y && mv /var/www/html/index.html /var/www/html/index.html.old && echo "Meu primeiro site hospedado via Docker" > /var/www/html/index.html
                EXPOSE 80
                CMD apache2ctl -D FOREGROUND
        
        ! docker build -t [seu_docker_id]/apache2_3rm2021s2 .
            docker images

        ! docker run -d -p 80:80 --name srvweb [seu_docker_id]/apache2_3rm2021s2
            docker ps

            <> Teste no navegador do Win10
                http://192.168.100.124/

        ! docker exec -it srvweb bash
             cd /var/www/html
             ls

            <> Alterar o aqruivo de configuração
                 echo *alterado enquanto funcionava* > index.html

        ! docker login -u [seu_usuário]

            <> Enviar a imagem criada em seu repositório
                 docker push [seu-docker-id]/apache2_3rm2021s2
