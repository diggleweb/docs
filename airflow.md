# AirFlow - agendador

## Conceitos importantes

- **ETL / Extract, Transform, Load**, Procedimento geral para copiar de uma ou mais fontes de dados para um destino específico.

- **DAG / Directed Acyclic graph**, Coleção de todas as tarefas a ser executadas, organizadas de forma que reflete a relação e dependencias emtre elas.

- **Operator**, Enquanto a DAG define o fluxo vai rodar, operador define o que será feito

- **TASK**, Uma instalcia de um Operador em execucão.

- **Worker**, Unidade de trabalho (processo, container, servico) que realiza o procesamento de uma tarefa de cada vez.

- **SCHEDULER**, Unidade de agendamento requerido para orquestrar a execução de trabalhos agendados.

- **WEBSERVER**, Servidor de interface web.

- **BROKER**, armazena as filas de tarefas a serem executadas.

## Apache AirFlow

- plataforma open source que agenda e executa tarefas em codigo python
- gerenciamento de fluxos
    fluxo de tarefas:
    - intervalo de eexecucao
    - status de tarefas

## Executore (servicos embutidos)

    - **SequencialExecutor** (somente para teste)
        - uma unica task de uma vez
        - indicado para ambiente de desenvolvimento
        - faci de debugar e entender o funcionamento do workflow

    - **LocalExecutor** (Configuracao mais simple e limitada)
        - Executa utilizando multiprocessos no host
        - Atende pequenas demandas

    - **DaskExecutor** (requer um cluster Dask e conf de host e port do cluster)
        - Utiliza a estructura de paralelistmo da ferramenta Dask (pandas comprocesamento distribuido)
        - Demandas especificas de Data Science (grandes volumens de dados)

    - **CeleryExecutor** (Requer configuração de Celery banckend: redis ou rabbitmq)
        - Processamento utilizando multi host
        - Otimizado para produção
        - Utiliza a engine Celery ([](http://celeryproject.org/)) para tarefas distribuidas
        - capacidade de procesamento limitada apenas pela infraestructura.

    - **KubernetesExecutor** (requer configuracao de um kluster k8s)
        - Utiliza a arquitetura do Kubernetes para procesamento das task.

    - **debugExecutor** (Somente para testes)

## install airflow in mac

- criando um ambiente virtual
    > cd ~

    > mkdir airflow && cd airflow

    > python3.7 -m pip install virtualenv

    > virtualenv -p python3 venv

    > source venv/bin/activate

- install airflow

    > pip3 install apache-airflow

    criar novo diretorio
    > mkdir airflow && cd airflow

        export variable de ambiente
        
        ```
        export AIRFLOW_HOME=/Users/alexyucra/airflow/airflow
        ```
        para quem usa o bach zsh:

        > sudo nano ~/.zshrc

        adicione a seguinte lina

        ```
        export AIRFLOW_HOME=/Users/alexyucra/airflow/airflow
        ```
        
        reinicie bach
        > source ~/.zshrc 

        sair da pasta airflow
        > cd ..
    ativar novamente o ambiente virtual
    > source venv/bin/activate

    iniciar os metadados  DAG salvos no db em sqlite.
    > airflow db init

    run em outro terminal, exportando a variable de ambiente
    > airflow scheduler

    run 
    > airflow webserver
r
- Install user admin
    > FLASK_APP=airflow.www.app flask fab create-admin

    seiga as instruções:
    ```
    Username [admin]:
    User first name [admin]:
    User last name [user]:
    Email [admin@fab.org]:
    Password: 
    ```

- configure variable de ambiente

    > mkdir -p ./dags ./logs ./plugins
    > echo -e "AIRFLOW_UID=$(id -u)\nAIRFLOW_GID=0" > .env

    ```
    AIRFLOW_UID=501
    AIRFLOW_GID=0
    ```
- verificar versoes
    > docker exec <id_conatiner> airflow version


- error de coneccion com mysql
    
    ```
    # mac
    /Applications/xampp/xamppfiles/bin/mysql -uroot -p
    mysql> mysql -uroot -p
    mysql> create database airflow;
    mysql> grant all on airflow.* to 'airflow'@'localhost' identified by 'admin123';
    mysql> flush privileges;
    mysql> grant all on airflow.* to 'airflow'@'%' identified by 'admin123';
    mysql> flush privileges;

    mysql> show global variables like '%timestamp%';
    +---------------------------------+-------+
    | Variable_name                   | Value |
    +---------------------------------+-------+
    | explicit_defaults_for_timestamp | OFF   |
    | log_timestamps                  | UTC   |
    +---------------------------------+-------+
    2 rows in set (0.00 sec)

    mysql> set global explicit_defaults_for_timestamp =1;
    Query OK, 0 rows affected (0.00 sec)
    ```

    setup admin user
    ```
    airflow users create \
    --username admin \
    --firstname Alex \
    --lastname Yucra \
    --role Admin \
    --email xalextrack@gmail.com
    ```

    run server 
    > airflow webserver --port 8090 -D

    start Scheduler
    > airflow scheduler

### configure airflow

> nano /Users/alexyucra/airflow/airflow/airflow.cfg

- configurar user admin

    > FLASK_APP=airflow.www.app flask fab create-admin

- reiniciar servicos com docker
    > docker-compose down && docker-compose up

### Configure mysql para o backend

    ```sql
    CREATE DATABASE airflow_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
    CREATE USER 'airflow_user' IDENTIFIED BY 'airflow_pass';
    GRANT ALL PRIVILEGES ON airflow_db.* TO 'airflow_user';
    ```

    no arquivo de configuracao adicione a seguinte linha:
    `mysql+mysqlconnector://<user>:<password>@<host>[:<port>]/<dbname>`

## API AIRFLOW

- listar dags
    > curl -X GET "http://localhost:8080/api/v1/dags"
    
    ```json
    {
        "detail": null,
        "status": 401,
        "title": "Unauthorized",
        "type": "https://airflow.apache.org/docs/apache-airflow/2.1.3/stable-rest-api-ref.html#section/Errors/Unauthenticated"
    }
    ```

    > curl -X GET --user "airflow:airflow" "http://localhost:8080/api/v1/dags"

## Single node

- Single node
    
    ![](img/single_node.png)

- Single node celery

    ![](img/single_node_celery.png)

- Multi node celery

    ![](img/multi_node_celery.png)

- K8s cluster

    ![](img/kubernete_cluster.png)

___
## bibliografia

- [como instalar airflow en mac](https://my330space.wordpress.com/2019/12/20/how-to-install-apache-airflow-on-mac/)

- [airflow step by step](https://progressivecoder.com/step-by-step-guide-to-install-airflow/)

- [Install apache airflow on centos 7](https://0x0ece.medium.com/installing-apache-airflow-on-centos-7-750c77b7aa35)