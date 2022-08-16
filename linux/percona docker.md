# percona docker
O que é PMM
O PMM é uma ferramenta de monitoramento que pode monitorar MySQL, PostgreSQL, MongoDB, etc.
O PMM Client instalado no host do banco de dados coleta dados do banco de dados e do host.
O PMM Server agrega os dados coletados pelo PMM Client e os exibe em um gráfico.

# Versão do software
- Docker 19.03.5
- MySQL 8.0.19
- PMM 2.2.2
O servidor PMM (pmm-1) e o cliente PMM (pmm-2) devem poder se comunicar para coletar dados.
Para habilitar a comunicação, abra as seguintes portas.

pmm-1 libera a porta 80 ou 443 para pmm-2
pmm-2 libera as portas 42000 e 42001 para o pmm-1

# percona docker [ https://morganwu277.github.io/2017/12/26/Install-Percona-Monitoring-and-Management-System/ ]

https://www.percona.com/doc/percona-monitoring-and-management/2.x/install/docker-setting-up.html

docker pull percona/pmm-server:2

docker create \
   -v /srv \
   --name pmm-data \
   percona/pmm-server:2 /bin/true

docker run -d \
  -p 8081:80 \
  -p 443:443 \
  --volumes-from pmm-data \
  --name pmm-server \
  -e ORCHESTRATOR_ENABLED=true \
  -e ORCHESTRATOR_USER=pmmuser  \
  -e ORCHESTRATOR_PASSWORD=XXXX \
  -e DISABLE_UPDATES=true \
  --restart always \
  percona/pmm-server:2

# install pmm client en centoOS

## descarga

sudo yum install https://repo.percona.com/yum/percona-release-latest.noarch.rpm

## se for instalado mas veces

sudo percona-release disable all
sudo percona-release enable original release

## install
yum install pmm2-client

# configure pmm-admin config --server-insecure-tls --server-url=https://admin:admin@<IP Address>:443

pmm-admin config --server-insecure-tls --server-insecure-tls --server-url=http://admin:admin@10.0.1.7:443
pmm-agent setup --server-insecure-tls --server-address=10.0.1.7:443

server:
client:

/bin/pmm-agent setup --config-file=config/pmm-agent.yaml \
--paths-node_exporter="$PWD/bin/node_exporter" \
--paths-mysqld_exporter="$PWD/bin/mysqld_exporter" \
--paths-mongodb_exporter="$PWD/bin/mongodb_exporter" \
--paths-postgres_exporter="$PWD/bin/postgres_exporter" \
--paths-proxysql_exporter="$PWD/bin/proxysql_exporter" \
--server-insecure-tls --server-address=192.168.0.54:443 \
--server-username=admin  --server-password="admin" 192.168.0.136 generic node8.ca


