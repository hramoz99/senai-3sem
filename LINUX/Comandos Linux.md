# LINUX
```
  [usuário]@[nome da máquina]: ~# **(root)**
  
  [usuário]@[nome da máquina]: ~$ **(usuário)**
```
    

### COMANDOS

#### APRESENTAÇÃO DO USUÁRIO LOGADO 
```
whoami
```

#### INFORMAÇÕES DE PROCESSAMENTO
```
who -u
```

#### ENTRAR COM USUÁRIO ROOT
```
sudo su -
```


#### MOVIMENTAÇÃO ENTRE PASTAS/ARQUIVOS
```
cd [pasta]
 
    *control a = vai para o inicio da linha
    *control e = vai para o fim da linha 
    *control l = clear
    *control d = exit
```

#### VERIFICAR O DIRETÓRIO ATUAL 
```
pwd
```

#### LIMPAR A TELA 
```
clear ou ctrl + l
```

#### CRIAR PASTAS
```
mkdir [nome_da_pasta]
```

#### CRIAR PASTA E SUB-PASTAS SIMULTANEAMENTE
```
mkdir -p [pasta]/[sub_pasta]
```

#### APAGAR ARQUIVOS 
```
rm [nome_do_arquivo] 
```

#### APAGAR PASTA
```
rm -r [nome_da_pasta]
```

#### VISUALIZAR ARQUIVOS 
```
cat [caminho]
```

#### PARÂMETRO DE BUSCA DE ARQUIVOS - **find**
```
find [diretório] -name <nome_do_arquivo_ou_pasta>
      
        EX: find /etc/-name.conf
```

#### COPIAR ARQUIVOS 
```
cp <arquivo_de_origem> <arquivo_de_destino>
```

#### COPIAR PASTAS
```
cp -r <arquivo_de_origem> <arquivo_de_destino>
```

#### MOVER ARQUIVOS E PASTAS 
```
mv <pasta_caminho> <pasta_destino>
```

#### ADICIONAR USUÁRIO
```
adduser [nome_do_usuário]
UID - Identificação numérica única do Usuário
```

#### DELETAR USUÁRIO
```
deluser [nome_do_usuário]
```

#### ADICIONAR GRUPO 
```
addgroup [nome_do_grupo]
GID - Identificação numérica única do Grupo
```

#### DELETAR GRUPO
```
delgroup [nome_do_grupo]
```

#### TROCAR A SENHA DE UM USUÁRIO
```
passwd
```

#### SEPARAÇÃO DE USUÁRIO POR GRUPO
```
adduser [usuario] [grupo] 
deluser [usuario] [grupo] 
```

#### EXIBIR AS ÚLTIMAS 10 LINHAS DE UM ARQUIVO
```
tail
```

#### EXIBIR AS ÚLTIMAS LINHAS DE UM ARQUIVO EM TEMPO REAL
```
tail -f 
```

#### FILTRAR INFRMAÇÕES ESPECÍFICAS DE UM ARQUIVO 
```
grep (junto com |)
```

#### TROCAR O USUÁRIO DONO DA PASTA/ARQUIVO
```
chown [usuario] [pasta/arquivo]

 OBS: Para trocar usuário e grupo dona da pasta ao mesmo tempo **chown usuario:grupo [pasta/arquivo]
```

#### TROCAR O GRUPO DONO DA PASTA/ARQUIVO
```
chgrp [grupo] [pasta/arquivo]

 OBS: Para trocar os grupos donos de uma vez use **chgrp -R**
```

#### TROCAR AS PERMISSÕES DE UMA PASTA/ARQUIVO 
```
chmod [permissao] [pasta/arquivo]



     **Permissões**

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
#### LISTAR OS DIRETÓRIOS E SUBDIRETÓRIOS
```
ls -lR
    
    *Arquivo com inicial d = diretório
    *Arquivo com inicial l = link
    *Arquivo com inicial c = caractér
    *Arquivo com inicial b = dispositivo de bloco
    *Arquivo com inicial - = arquivo simples
    *Arquivo com inicial s = comunicação do SO com um pc
```
#### LISTAR OS DIRETÓRIOS E DIRETÓRIOS OCULTOS
```
ls -la
```

#### EDITORES DE TEXTO PARA O TERMINAL
```
    
    **nano**

        Pesquisar: Ctrl+W
        Copiar = Alt+6
        Recortar = Ctrl+K
        Colar = Ctrl+U

        Salvar = Ctrl+O
        Sair = Ctrl+X

        Desfazer = Alt+U

    **vim** (Versão otimizada do 'vi')

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
   

#### NOME DAS INTERFACES 
```
lo - Loopback
enp0s3 - Interface de Rede (Padrão antigo - eth0)
```

#### VISUALIZAR INFORMAÇÕES DE REDE 
```
ip add
ifconfig (instalar apt-get install "net-tools")
```

#### LIMPAR E SOLICITAR UM ENDEREÇO IP NOVO PARA O DHCP
```
ip add flush dev <nome_da_interface>
   
  Exemplo: ip add flush dev enp0s3
```

### LIGAR E DESLIGAR UMA INTERFACE ESPÉCIFICA

#### DESLIGAR UMA INTERFACE 
```
ifdown [nome_da_interface]
```

#### LIGAR UMA INTERFACE 
```
ifup [nome_da_interface]
```

#### VISUALIZAR OS DISCOS EXISTENTES
```
fdisk -l
```

#### VISUALIZAR OS DISCOS EM EXECUÇÃO
```
df -h
```

#### CRIAR ARQUIVOS VAZIOS
```
touch [nome_do_arquivo]
    
  EX: touch /mnt/disco2G/arquivo2.txt

```
#### DELISGAR A MÁQUINA 
```
init 0 
```

#### DEFINIR HORÁRIO PARA A MÁQUINA DESLIGAR 
```
Shutdown -h [horário] 
```

#### REINICIAR A MÁQUINA 
```
reboot
```
#### VISUALIZAR UMA VARIÁVEL 
```
echo $[nome_da_variável]
```


#### VISUALIZAR TODAS VARIÁVEIS
```
set 
```

#### ABREVIAÇÃO DE COMANDOS 
```
alias 
  EXEMPLO = comando completo [iptables -t nat -nL]
            abreviado [alias nat = "iptables -t nat -nL"]
```

#### INFORME OS 16 COMANDOS SELECIOANDOS ANTERIORMENTE
```
fc -l
```

#### INFORME OS COMANDOS SELECIONADOS ANTERIORMENTE
```
history [valor]
```

#### VERSÃO DO KERNEL
```
uname -a
```


#### EXPLICAÇÃO A FUNÇÃO DO COMANDO 
```
help [comando] 
```

#### EXPLORAÇÃO AMPLA DA PALAVRA CHAVE 
```
apropos [palavra_chave]
```

#### EXPLORAÇÃO ESPECÍFICA DA PALAVRA CHAVE 
```
whatis <palavra_chave>
```

#### MANUAL DO COMANDO 
```
man [comando]
```

#### MANUAL DO ARQUIVO DE CONFIGURAÇÃO 
```
man [seção] [comando]
```

#### CONSULTA DE COMANDOS
```
xman 
```
 
#### PASTA/MANUAL DO COMANDO 
```
whereis [comando] 
```
     
#### CRIA NOVOS ARQUIVOS 
```
touch [nome_do_arquivo]
```   

#### CARACTERÍSTICAS DE UM ARQUIVO 
```
stat <nome_do_arquivo.extensão>
```

#### EMPACOTADOR DE ARQUIVOS
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

#### COMPACTADOR DE ARQUIVOS 
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
  
#### LISTAR TODOS PROCESSOS 
```
top ou htop
```

#### PARAR PROCESSO 
```
Ctrl+Z
```

#### VOLTAR OS PROCESSOS *PARADOS*
```
fg [número_do_processo]
```

#### VISUALIZAR PROCESSOS *PARARDO*
```
jobs
```

#### MATAR QUALQUER PROCESSO 
```
kill [número_do_processo]
```

#### CRIAR PROCESSOS/PRIORIDADE
```
nice
```


#### ALTERAR PROCESSOS/PRIORIDADE 
```
renice
```





 


               
            
   
