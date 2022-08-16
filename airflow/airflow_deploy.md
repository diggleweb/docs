# Install airflow with docker in centos

## Obtendo informacões da minha distro

Primero de tudo vou comezar verificando a distro de disponho para realizar meus analise.

> cat /proc/version

> cat /etc/*release*

> lsb_release -a

> gcc --version

> uname -a

> python -c 'import platform; print(platform.dist()[0])'

## criar novo usuario no CentOS

listar usuarios linux
> $ `cat /etc/passwd`

> $ `adduser mynewuser` # new user

> $ `passwd mynewuser` # change password

> ssh airflow@<ip_host> 

listar portas abertas como root
> firewall-cmd --list-all

abrir as portas 8080 e 5555
> firewall-cmd --zone=public --permanent --add-port 8080/tcp

> firewall-cmd --zone=public --permanent --add-port 5555/tcp

> firewall-cmd --reload

## inicializar 


Criar pasta dentro de uma pasta `airflow``
> mkdir -p ./dags ./logs ./plugins

crie variable de ambiente
> echo -e "AIRFLOW_UID=$(id -u)\nAIRFLOW_GID=0" > .env

crie variable de ambiente para postgres
>  echo -e "POSTGRES_USER=airflow\nPOSTGRES_PASSWORD=airflow\nPOSTGRES_DB=airflow" > postgres.env


## firewalld

> systemctl is-active docker

> systemctl start docker

verificar servicos docker
> systemctl status docker 

## airflow como service

crei um arquivo no seguinte caminho
> sudo touch /lib/systemd/system/airflow-webserver.service

> sudo nano /lib/systemd/system/airflow-webserver.service

```shell
# service name:     airflow-webserver.service
# path:             /lib/systemd/system/airflow-webserver.service

[Unit]
Description="airflow webserver run in port 8080"

[Service]
Type=simple
PIDFile=/run/airflow-webserver.pid

#EnvironmentFile=/home/airflow/airflow/.env

# Jupyter Notebook: change PATHs as needed for your system
ExecStart=/home/airflow/airflow/airflow.sh --logging.dest="/var/log/airflow/airflow-webserver.log"
# ExecStart=

# User=airflow
# Group=airflow
WorkingDirectory=/home/airflow/airflow
Restart=always
RestartSec=10
#KillMode=mixed

[Install]
#WantedBy=multi-user.target
```

## chmod para tornar executable

> chmod +x run.sh
> ./run.sh

run service
> systemctl daemon-reload

- verifique se os container estao rodando, se nao:
    > docker-compose up -d

> systemctl enable --now airflow-webserver.service

> systemctl start airflow-webserver.service

## debug systemctl

> yournalctl -u -f <nome_servico>


## addicionar docker ao usuario criado

> sudo groupadd docker

> usermod -aG docker airflow

## install in centos8 

erro: overcommit_memory is set to 0 [https://access.redhat.com/documentation/pt-br/red_hat_enterprise_linux/6/html/performance_tuning_guide/s-memory-captun](https://access.redhat.com/documentation/pt-br/red_hat_enterprise_linux/6/html/performance_tuning_guide/s-memory-captun)

To fix this issue add 'vm.overcommit_memory = 1' to /etc/sysctl.conf

> sudo echo -e "\nvm.overcommit_memory = 1" > /etc/sysctl.conf
