#! / bin / bash

#### DECLARAR A POLÍTICA PADRÃO PARA PERMISSIVA
```
iptables -P INPUT ACCEPT
iptables -P SAÍDA ACCEPT
iptables -P FORWARD ACCEPT
```

#### LIMPAR AS CHAINS DA TABELA FILTER
```
iptables -F
```
#### LIMPAR A CONSOLE E APRESENTAR A CONFIGURAÇÃO ATUAL
```
Clear
iptables -L -nv
```
