# SCRIPT - CISCO ASA
__________________________________________________

              IP dos PCs -> segundo IP válido
              
___________________________________________________
#### Configuração das interfaces
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
#### Definição dos níveis de segurança das interfaces
```
int g1/1
security-level 0
int g1/2
security-level 0
int g1/3
security-level 0
```

#### Definir ZONA INTERMEDIÁRIA - 'DMZ' 
```
int g1/1
security-level 0
int g1/2
security-level 50
int g1/3
security-level 100
```

#### Ligar a placa de Rede - GERENCIAMENTO 
```
interface management 1/1
nameif gerencia
security-level 0
ip add 172.16.0.1
no sh
```

#### Criação do Acesso SSH
```
username admin password Senai@132
ssh 172.16.0.0 255.255.0.0 gerencia
aaa authentication ssh console LOCAL
ssh timeout 60
```

#### Permitir PING da INTERNET - 'DMZ' 
```
access-list T1 extend permit icmp host 192.168.10.2 host 192.168.20.2
access-group T1 in interface a
```

#### Permitir PING da INTERNET LOCAL - LAN
```
access-list T1 extend permit icmp host 192.168.10.2 host 192.168.1.2
```

#### Apagar as regras para a liberação de ICMP para toda rede  
```
no access-list T1 extend permit icmp host 192.168.10.2 host 192.168.20.2
no access-list T1 extend permit icmp host 192.168.10.2 host 192.168.1.2
!
access-list T1 extend permit icmp any any
access-group T1 in interface a
access-group T1 in interface b
```

#### Salvar as configurações 
```
write memory
```
