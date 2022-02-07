# LINUX
```
  [usuário]@[nome da máquina]: ~# (root)
  
  [usuário]@[nome da máquina]: ~$ (usuário)
```

## Caminhos
#### Arquivo que armazena o nome do Computador 
```
/etc/hostname
``` 

#### Arquivo que contém os usuários LINUX 
```
/etc/passwd
```


#### Arquivos que contém os grupos
```
/etc/group
```


#### Arquivo que contém os usuários 
```
/etc/shadow 
```


#### Arquivo de armazenamento dos LOGs do sistema
```
/var/log/syslog 
```

#### Arquivo de armazenamento de autenticação de usuários 
```
/var/log/auth.log
```

#### Nome das interfaces
```
lo - Loopback
enp0s3 - Interface de Rede [Padrão antigo era eth0]
```

#### Arquivo que contém as configurações das interfaces de REDE
```
/etc/network/interfaces


    <> Configurar IP Estático

        auto [nome-da-interface]
        iface [nome-da-interface] inet static
            address [endereco-ip]/[máscara]

     <> Outras parêmetros: gateway, broadcast, nameserver.

         auto [nome-da-interface]
         iface [nome-da-interface] inet static
            address [endereco-ip]/[máscara]
            gateway [endereco-ip-do-gateway]
            nameserver [endereco-ip-do-dns]

```

#### LOG de Erros
```
journalctl -xe
```

#### Habilitação do Apache - BootStraping (automatização)
```
#!/bin/bash
yum -y install httpd
systemctl enable httpd
systemctl start httpd
echo '<html><h1>Senai Informática e AWS a parceria do futuro! </h1></html>' > /var/www/html/index.html
```

#### Editar o APACHE 
```
vim ou nano /var/www/html/index.html  
```

#### Adicionar novas Chaves SSH
```
vim ou nano /home/ec2-user/.ssh/authorized_keys
```

#### Criare uma nova partição no DISCO 
```
fdisk /dev/xvdf

n> p> enter> enter> enter> w
```

#### Formatação de partição 
```
mkfs -t ext3 /dev/xvdf1
```

#### Criar um diretório para a nova partição
```
mkdir /mnt/novo-disco
```

#### Criar um arquivo para vizualização de BACKUP 
```
nano /mnt/novo-disco/arquivo.txt
```

#### Criar um ponto de montagem
```
mkdir /mnt/disco2G
```

#### Montar a partição no diretório adicionado
```
mount /dev/xvdf1 /mnt/disco2G
```

#### Criar arquivos vazios
```
touch /mnt/disco2G/arquivo2.txt (exemplo)
```

#### Restaurar o Backup
```
cp -a /mnt/disco2G/* /mnt/novo-disco30G/
```

#### Instalar pacotes
```
apt install [nome_do_pacote]
```

#### Atualizar pacotes  
```
apt upgrade
```

#### Atualizar pastas e arquivos 
```
apt update
```

#### Procurar arquivos 
```
apt-cache search [nome_do_pacote]
```


#### Verificar se o pacotes está instalado 
```
aptitude search [nome_do_pacote]
```

#### Instalar, atualizar e procurar pacotes disponíveis 
```
apt-get remove [nome_do_pacote] --purge
```
