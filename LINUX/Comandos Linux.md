# LINUX
```
  [usuário]@[nome da máquina]: ~# (root)
  
  [usuário]@[nome da máquina]: ~$ (usuário)
```
    

### `COMANDOS`

#### Apresentação do usuário logado 
```
whoami
```

#### Informação de processamento 
```
who -u
```

#### Entrar com usuário ROOT
```
sudo su -
```


#### Movimentação entre pastas/arquivos
```
cd [pasta]
 
    *control a = vai para o inicio da linha
    *control e = vai para o fim da linha 
    *control l = clear
    *control d = exit
```

#### Verificar o diretório atual
```
pwd
```

#### Limpar a tela 
```
clear ou ctrl + l
```

#### Criar pastas
```
mkdir [nome_da_pasta]
```

#### Criar pasta e sub-pastas SIMULTANEAMENTE
```
mkdir -p [pasta]/[sub_pasta]
```

#### Apagar arquivos 
```
rm [nome_do_arquivo] 
```

#### Apagar pasta
```
rm -r [nome_da_pasta]
```

#### Visualizar arquivos 
```
cat [caminho]
```

#### Parâmetro de busca de arquivos - **find**
```
find [diretório] -name <nome_do_arquivo_ou_pasta>
      
        EX: find /etc/-name.conf
```

#### Copiar arquivos 
```
cp <arquivo_de_origem> <arquivo_de_destino>
```

#### Copiar pastas 
```
cp -r <arquivo_de_origem> <arquivo_de_destino>
```

#### Mover arquivos e pastas 
```
mv <pasta_caminho> <pasta_destino>
```

#### Adicionar usuário 
```
adduser [nome_do_usuário]
UID - Identificação numérica única do Usuário
```

#### Deletar usuário 
```
deluser [nome_do_usuário]
```

#### Adicionar grupo 
```
addgroup [nome_do_grupo]
GID - Identificação numérica única do Grupo
```

#### Deletar grupo
```
delgroup [nome_do_grupo]
```

#### Trocar a senha de um usuário
```
passwd
```

#### Separação de usuário por grupo
```
adduser [usuario] [grupo] 
deluser [usuario] [grupo] 
```

#### Exibir as últimas 10 linhas de um arquivo
```
tail
```

#### Exibir as últimas linhas de um arquivo em tempo real 
```
tail -f 
```

#### Filtrar informações específicas de um arquivo
```
grep (junto com |)
```

#### Trocar o usuário DONO da pasta/arquivo
```
chown [usuario] [pasta/arquivo]

 OBS: Para trocar usuário e grupo dona da pasta ao mesmo tempo **chown usuario:grupo [pasta/arquivo]
```

#### Trocar o grupo DONO da pasta/arquivo
```
chgrp [grupo] [pasta/arquivo]

 OBS: Para trocar os grupos donos de uma vez use **chgrp -R**
```

#### Trocar as permissões de uma pasta/arquivo 
```
chmod [permissao] [pasta/arquivo]



     Permissões

    d     rwx        rwx      rwx
       U[suario]   G[rupo]   O[utros]
    r - ler
    w - escrever
    x - executar

    desenvolvimento - d rwx r-x r-x [Permissão antiga]
                        111 101 101
                         7   5   5
    desenvolvimento - d rwx rwx r-x [Permissão nova]
                        111 111 101
                         7   7   5

    

	       ---------------------------------------
	        número    binário equiv.   permissões
	       ---------------------------------------
                0           000            ---
                1           001            --x
                2           010            -w-
                3           011            -wx
                4           100            r--
                5           101            r-x
                6           110            rw-
                7           111            rwx
	       ---------------------------------------
```
#### Listar os diretórios e subdiretórios 
```
ls -lR
    
    * Arquivo com inicial d = diretório
    * Arquivo com inicial l = link
    * Arquivo com inicial c = caractér
    * Arquivo com inicial b = dispositivo de bloco
    * Arquivo com inicial - = arquivo simples
    * Arquivo com inicial s = comunicação do SO com um pc
```
#### Listar os diretórios e diretórios ocultos
```
ls -la
```

#### Editores de texto para o terminal
```
    
    nano

        Pesquisar: Ctrl+W
        Copiar = Alt+6
        Recortar = Ctrl+K
        Colar = Ctrl+U

        Salvar = Ctrl+O
        Sair = Ctrl+X

        Desfazer = Alt+U

    vim (Versão otimizada do 'vi')

        : = Inserir comando
        i = Entrar no modo de Inserção
        :w = Salvar o arquivo
        :q = Sair do arquivo
        :q! = Salvar de maneira "forçada"
        :wq = Salvar e sair
         v = Entrar no modo visual
         y = Copiar
         p = Colar
         u = Desfazer
         H = Cursor vai para a primeira linha do arquivo
         dd = Deleta a linha 
         set nu = Numerar as linhas
```        
   

#### Nome das interfaces 
```
lo - Loopback
enp0s3 - Interface de Rede (Padrão antigo - eth0)
```

#### Visualizar informações de rede 
```
ip add
ifconfig (instalar apt-get install "net-tools")
```

#### Limpar e solicitar um endereço IP novo para o DHCP
```
ip add flush dev <nome_da_interface>
   
  Exemplo: ip add flush dev enp0s3
```

### LIGAR E DESLIGAR UMA INTERFACE ESPÉCIFICA

#### Desligar uma interface 
```
ifdown [nome_da_interface]
```

#### Ligar uma interface 
```
ifup [nome_da_interface]
```

#### Visualizar os discos existentes 
```
fdisk -l
```

#### Visualizar os discos em execução 
```
df -h
```

#### Criar arquivos vazios 
```
touch [nome_do_arquivo]
    
  EX: touch /mnt/disco2G/arquivo2.txt

```
#### Desligar a máquina 
```
init 0 
```

#### Defnir horário para a MÁQUINA desligar 
```
Shutdown -h [horário] 
```

#### Reiniciar a MÁQUINA 
```
reboot
```
#### Visualizar uma variável
```
echo $[nome_da_variável]
```


#### Visualizar todas variáveis 
```
set 
```

#### Abreviação de comandos 
```
alias 
  EXEMPLO = comando completo [iptables -t nat -nL]
            abreviado [alias nat = "iptables -t nat -nL"]
```

#### Informe os 16 comandos selecionados ANTERIORMENTE
```
fc -l
```

#### Informe os comandos selecionados ANTERIORMENTE 
```
history [valor]
```

#### Versão do KERNEL
```
uname -a
```


#### Explicação a função do comando 
```
help [comando] 
```

#### Explorador amplo da palavra chave 
```
apropos [palavra_chave]
```

#### Exploração específica da palavra chave 
```
whatis <palavra_chave>
```

#### Manual do comando 
```
man [comando]
```

#### Manual do aruqivo de configuração 
```
man [seção] [comando]
```

#### Consulta de comandos 
```
xman 
```
 
#### Pasta/Manual do Comando
```
whereis [comando] 
```
     
#### Cria novos arquivos 
```
touch [nome_do_arquivo]
```   

#### Características de um arquivo
```
stat <nome_do_arquivo.extensão>
```

#### Empacotador de arquivos 
```
tar [opções] <dispositivo/arquivo> <arquivo1> <arquivo2>
 
     Opções
         *-c ou -create  - inicia o empacotamento no arquivo
         *-f ou file     - reconhece o arquivo como próprio do sistema
         *-j ou -bzip2   - compacta o arquivo no momento do empacotamento (bzip2)
         *-J ou -xz      - compacta o arquivo no momento do empacotamento (xz)
         *-v ou -verbose - exibi todo o processo de empacotamento/desempacotamento
         *-t ou -list    - visualizar o conteúdo do pacote
         *-x ou -extract - desempacota o arquivo ou extrai o conteúdo de um pacote tar
```

#### Compactador de arquivos 
```
 gzip [opções] <arquivo>
 
     Opções
         *-c ou -stdout      - compacta o arquivo original
         *-d ou -decompress  - descompacta os arquivos .gzip
         *-f ou -force       - força a compactação/descompactação
         *-l ou -list        - exibi informações detalhadas sobre o arquivo compactado/descompactado
         *-t ou -test        - testa a integridade do arquivo
         *-v ou -verbose     - exibi o processo de compactação/descompactação
         *-<nivel> ou -fast  - tamanho da compactação
   ```          
  
#### Listar todos processos
```
top ou htop
```

#### Parar processos
```
Ctrl+Z
```

#### Voltar os processos *PARADOS*
```
fg [número_do_processo]
```

#### Visualizar processos *PARARDO*
```
jobs
```

#### Matar qualquer processo 
```
kill [número_do_processo]
```

#### Criar processos/prioridade
```
nice
```


#### Alterar processos/prioridade
```
renice
```





 


               
            
   
