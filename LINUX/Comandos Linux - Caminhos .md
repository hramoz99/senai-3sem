# LINUX - Caminhos

!ARQUVIVOARMANZENA O NOME DO COMPUTADOR
/etc/hostname


!ARQUIVO QUE CONTÉM OS USUÁRIOS DO LINUX
/etc/passwd 


!ARQUIVO que contém os grupos do Linux ARQUIVO
/etc/group


!ARQUIVO que contém as senhas dos usuários
/etc/shadow 


!ARQUIVO de armazenamento dos Logs do Sistema
/var/log/syslog 


!ARQUIVO DE ARMAZENAMENTO DE AUTENTICAÇÃO DE USUÁRIOS
/var/log/auth.log


!NOME DAS INTERFACES
lo - Loopback
enp0s3 - Interface de Rede [Padrão antigo era eth0]


!ARQUIVO QUE CONTÉM AS CONFIGURAÇÕES DAS INTERFACES DE REDE
/etc/network/interfaces


    **Configurar IP Estático**

        auto [nome-da-interface]
        iface [nome-da-interface] inet static
            address [endereco-ip]/[máscara]

        Outras possibilidades de parêmetros: gateway, broadcast, nameserver.

         auto [nome-da-interface]
         iface [nome-da-interface] inet static
            address [endereco-ip]/[máscara]
            gateway [endereco-ip-do-gateway]
            nameserver [endereco-ip-do-dns]



!LOG DE ERROS NOS SERVIÇOS LINUX
journalctl -xe


!HABILITAÇÃO DO APACHE- BootStraping (automatização)
#!/bin/bash
yum -y install httpd
systemctl enable httpd
systemctl start httpd
echo '<html><h1>Senai Informática e AWS a parceria do futuro! </h1></html>' > /var/www/html/index.html
 

!EDITAR O APACHE 
vim ou nano /var/www/html/index.html  


!ADICIONAR NOVAS CHAVES SSH
vim ou nano /home/ec2-user/.ssh/authorized_keys


!CRIAR UMA PARTIÇÃO NO DISCO
fdisk /dev/xvdf

n> p> enter> enter> enter> w


!FORMATAÇÃO DE PARTIÇÃO 
mkfs -t ext3 /dev/xvdf1


!CRIAR UM DIRETÓRIO PARA A NOVA PARTIÇÃO 
mkdir /mnt/novo-disco


!FINALIZAÇÃO
mount /dev/xvdf1 /mnt/novo-disco


!CRIAR UM ARQUIVO PARA VIZUALIÇÃO DE BACKUP 
nano /mnt/novo-disco/arquivo.txt


!CRIAR UM PONTO DE MONTAGEM 
mkdir /mnt/disco2G


!MONTAR A PARTIÇÃO NO DIRETÓRIO CRIADO
mount /dev/xvdf1 /mnt/disco2G


!CRIAR ARQUIVOS VAZIOS
touch /mnt/disco2G/arquivo2.txt (exemplo)


!RESTAURAR BACKUP
cp -a /mnt/disco2G/* /mnt/novo-disco30G/


!INSTALAR PACOTES
apt install [nome_do_pacote]


!ATUALIZAR PACOTES  
apt upgrade


!ATUALIZAR PASTAS E ARQUIVOS
apt update


!PROCURAR ARQUIVOS
apt-cache search [nome_do_pacote]


!VERIFICAR SE O PACOTE ESTÁ INSTALADO 
aptitude search [nome_do_pacote]


!INSTALAR PACOTES, ATUALIZAR E PROCURAR PACOTES DISPONIVEIS
apt-get remove [nome_do_pacote] --purge
