# mysql tuner 
  ===========
MysqlTuner é um script escrito em perl que lhe permite reconfigurar uma instalação MYSQL rapidamente e fazer ajustes para aumentar o desempenho e a estabilidade. As variáveis de configuração e status dos dados são mostrados em um formato simples, juntamente com algumas sugestões básicas para melhoria do desempenho.

git:
https://github.com/major/MySQLTuner-perl/blob/master/INTERNALS.md

### install mysqltuner.pl
'''
	> wget http://mysqltuner.com/mysqltuner.pl
	> chmod +x mysqltuner.pl
	> ./mysqltuner.pl
'''
## backup do /etc/mysql/my.cnf

sudo cp /etc/mysql/my.cnf /etc/mysql/my.cnf.bak

## when run results.

-- Log file Recommendations
-- Storage Engine Statistics
-- Analysis Performance Metrics
-- Security Recommendations
-- CVE Security Recommendations
-- Performance Metrics
-- Performance schema
-- ThreadPool Metrics
-- MyISAM Metrics
-- InnoDB Metrics
-- AriaDB Metrics
-- TokuDB Metrics
-- XtraDB Metrics
-- Galera Metrics
-- Replication Metrics
-- General recommendations

# reiniciar apos configuracoes do my.cnf

systemctl restart mysqld

______________________________________________
## key_buffer (alocação de mais memoria para Mysql)
monitoramento uso de memoria
mysql> SELECT * FROM performance_schema.setup_instruments
       WHERE NAME LIKE '%memory%';




# identificando paramatros que precisamos modificar para restringir o uso da memoria MYSQL
2 coisas que influencia direta ou indiretamente:
- memory por connection => maximo numero de conexcoes concurrentes
- innodbbufferpoolsize - sortbuffersize - readbuffersize - tmptablesize - maxconnections

# locate my.cnf
cat /etc/my.cnf.d/server.cnf | grep ^[A-Za-z]
cat /etc/my.cnf.d/client.cnf | grep ^[A-Za-z]
cat /etc/my.cnf.d/mysql-clients.cnf | grep ^[A-Za-z]

### como executar o scrip 
chmod a+x print-mem.sh
./script.sh

================= print-mem.sh =======================

#!/bin/sh
# you might want to add some user authentication here
mysql -e "show variables; show status" | awk '  
{
VAR[$1]=$2  
}
END {  
MAX_CONN = VAR["max_connections"]  
MAX_USED_CONN = VAR["Max_used_connections"]  
BASE_MEM=VAR["key_buffer_size"] + VAR["query_cache_size"] + VAR["innodb_buffer_pool_size"] + VAR["innodb_additional_mem_pool_size"] + VAR["innodb_log_buffer_size"]  
MEM_PER_CONN=VAR["read_buffer_size"] + VAR["read_rnd_buffer_size"] + VAR["sort_buffer_size"] + VAR["join_buffer_size"] + VAR["binlog_cache_size"] + VAR["thread_stack"] + VAR["tmp_table_size"]  
MEM_TOTAL_MIN=BASE_MEM + MEM_PER_CONN*MAX_USED_CONN  
MEM_TOTAL_MAX=BASE_MEM + MEM_PER_CONN*MAX_CONN
printf "+------------------------------------------+--------------------+\n"  
printf "| %40s | %15.3f MB |\n", "key_buffer_size", VAR["key_buffer_size"]/1048576  
printf "| %40s | %15.3f MB |\n", "query_cache_size", VAR["query_cache_size"]/1048576  
printf "| %40s | %15.3f MB |\n", "innodb_buffer_pool_size", VAR["innodb_buffer_pool_size"]/1048576  
printf "| %40s | %15.3f MB |\n", "innodb_additional_mem_pool_size", VAR["innodb_additional_mem_pool_size"]/1048576  
printf "| %40s | %15.3f MB |\n", "innodb_log_buffer_size", VAR["innodb_log_buffer_size"]/1048576  
printf "+------------------------------------------+--------------------+\n"  
printf "| %40s | %15.3f MB |\n", "BASE MEMORY", BASE_MEM/1048576  
printf "+------------------------------------------+--------------------+\n"  
printf "| %40s | %15.3f MB |\n", "sort_buffer_size", VAR["sort_buffer_size"]/1048576  
printf "| %40s | %15.3f MB |\n", "read_buffer_size", VAR["read_buffer_size"]/1048576  
printf "| %40s | %15.3f MB |\n", "read_rnd_buffer_size", VAR["read_rnd_buffer_size"]/1048576  
printf "| %40s | %15.3f MB |\n", "join_buffer_size", VAR["join_buffer_size"]/1048576  
printf "| %40s | %15.3f MB |\n", "thread_stack", VAR["thread_stack"]/1048576  
printf "| %40s | %15.3f MB |\n", "binlog_cache_size", VAR["binlog_cache_size"]/1048576  
printf "| %40s | %15.3f MB |\n", "tmp_table_size", VAR["tmp_table_size"]/1048576  
printf "+------------------------------------------+--------------------+\n"  
printf "| %40s | %15.3f MB |\n", "MEMORY PER CONNECTION", MEM_PER_CONN/1048576  
printf "+------------------------------------------+--------------------+\n"  
printf "| %40s | %18d |\n", "Max_used_connections", MAX_USED_CONN  
printf "| %40s | %18d |\n", "max_connections", MAX_CONN  
printf "+------------------------------------------+--------------------+\n"  
printf "| %40s | %15.3f MB |\n", "TOTAL (MIN)", MEM_TOTAL_MIN/1048576  
printf "| %40s | %15.3f MB |\n", "TOTAL (MAX)", MEM_TOTAL_MAX/1048576  
printf "+------------------------------------------+--------------------+\n"  
}'

============================ end sh =================================


### verificar:
- innodbbufferpoolsize 	(tam_tot buffer)
- sortbuffersize 		(tam_ordem buffer)
- readbuffersize 		(tam_leitura buffer)
- tmptablesize 			(tam_tabela tmp)
- maxconnections 		(conexiones maximas)

### configuracao inicial my.cnf
---------------
# 
# * Ajuste fino 
# 
key_buffer 			= 16M   
max_allowed_packet 	= 16M   
thread_stack 		= 192K   
thread_cache_size 	= 8   
# Isso substitui o script de inicialização e verifica as tabelas MyISAM, se necessário 
# na primeira vez em que são tocadas 
myisam-recover 		= BACKUP   
# max_connections 	= 100
---------------

mudar para 

---------------
# 
# * Fine Tuning 
# 
key_buffer 				= 16M   
read_buffer 			= 60K   
sort_buffer 			= 1M   
innodb_buffer_pool_size = 64M   
tmp_table 				= 8M   
max_allowed_packet 		= 16M   
thread_stack 			= 192K   
thread_cache_size 		= 8   
# Isto substitui as tabelas MyISAM de script de inicialização e verifica se necessário 
# a primeira vez que são tocados 
myisam -recover 		= BACKUP   
max_connections 		= 25
---------------

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
# Calcular o uso de memória Mysql

Estimativas ou cálculo de utilização de memória do MySQL com base nas variáveis ​​globais.

## formula:
	Uso da memória do servidor Mysql = Soma dos buffers globais + (número de conexões * varible de memoria por thread(tarefa)

## entendendo - Os buffers globais incluem:
key_buffer_size:					tamanho do buffer usado para blocos de índice.
innodb_buffer_pool_size:			tamanho em bytes do buffer de memória que o InnoDB usa para armazenar em cache os dados e os índices de suas tabelas.
innodb_additional_mem_pool_size:	tamanho em bytes de um pool de memória que o InnoDB usa para armazenar informações do dicionário de dados e outras estruturas de dados internas.
innodb_log_buffer_size:				tamanho em bytes do buffer que o InnoDB usa para gravar nos arquivos de log no disco.
query_cache_size:					quantidade de memória alocada para armazenar em cache os resultados da consulta.


Cada thread para conexão do cliente usa:

. thread_stack 			(tam_pilha para cada thread)
. net_buffer_length		(buffer de conexao)
. max_allowed_packet	(tam_max que net_buffer_length pode crescer)
. read_buffer_size 		(usado para barredura sequencial de tabela)
. read_rnd_buffer_size 	(usado para buffer de leitura aleatoria /classificação)
. tmp_table_size 		(tabelas temporarias / hash no mysql)
. sort_buffer_size 		(para classificar, agrupar, ordenar)

As variáveis por threads incluem
	. read_buffer_size: 
	. read_rnd_buffer_size:
	. sort_buffer_size:
	. join_buffer_size:	(tamanho do buffer usado para varreduras de índice simples, varreduras de índice de alcance e junções que não usam índices e, portanto, executam varreduras de tabela completas.)
	. thread_stack:
	. net_buffer_length:
	. max_allowed_packet:

# Buffer de cache:
  ================
  3 tipos de estado:
  . Dirty buffer (buffer sujos) - blocos de dados alterados debido a instrucao DML
  . Buffer livres (free buffer) - nao possuem dados
  . Pinned buffer (buffer fixados) - Buffers presos são buffers que estão em uso por declarações DML ou são explicitamente salvos para uso futuro e, portanto, não podem ser reutilizados.






