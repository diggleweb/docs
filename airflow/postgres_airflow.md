# verificar postgres no airflow

## ingresando no postgres

- verifique o id do container

example:

```
CONTAINER ID   IMAGE
-------------|------------
bc3fa6ed9fba   postgres:13
```

- ingreando no container

    $ docker exec -it <container_id> /bin/sh

-  ingresando no postgres usaremos como usuario=airflow senha= airflow

    $ psql -U airflow

    
``` shell
# listar todo slos bancos de dados
$ airflow> \l

                               List of databases
   Name    |  Owner  | Encoding |  Collate   |   Ctype    |  Access privileges  
-----------+---------+----------+------------+------------+---------------------
 airflow   | airflow | UTF8     | en_US.utf8 | en_US.utf8 | 
 postgres  | airflow | UTF8     | en_US.utf8 | en_US.utf8 | 
 template0 | airflow | UTF8     | en_US.utf8 | en_US.utf8 | =c/airflow         +
           |         |          |            |            | airflow=CTc/airflow
 template1 | airflow | UTF8     | en_US.utf8 | en_US.utf8 | =c/airflow         +
           |         |          |            |            | airflow=CTc/airflow
```

```
# listar de tabelas
$ airflow> \dt

                   List of relations
 Schema |             Name              | Type  |  Owner  
--------+-------------------------------+-------+---------
 public | ab_permission                 | table | airflow
 public | ab_permission_view            | table | airflow
 public | ab_permission_view_role       | table | airflow
 public | ab_register_user              | table | airflow
 public | ab_role                       | table | airflow
 public | ab_user                       | table | airflow
 public | ab_user_role                  | table | airflow
 public | ab_view_menu                  | table | airflow
 public | alembic_version               | table | airflow
 public | celery_taskmeta               | table | airflow
 public | celery_tasksetmeta            | table | airflow
 public | connection                    | table | airflow
 public | dag                           | table | airflow
 public | dag_code                      | table | airflow
 public | dag_pickle                    | table | airflow
 public | dag_run                       | table | airflow
 public | dag_tag                       | table | airflow
 public | import_error                  | table | airflow
 public | job                           | table | airflow
 public | log                           | table | airflow
 public | rendered_task_instance_fields | table | airflow
 public | sensor_instance               | table | airflow
 public | serialized_dag                | table | airflow
 public | sla_miss                      | table | airflow
 public | slot_pool                     | table | airflow
 public | task_fail                     | table | airflow
 public | task_instance                 | table | airflow
 public | task_reschedule               | table | airflow
 public | variable                      | table | airflow
 public | xcom                          | table | airflow

```

```
# listar de tabelas
$ airflow> \d variable
                                       Table "public.variable"
    Column    |          Type          | Collation | Nullable |               Default                
--------------+------------------------+-----------+----------+--------------------------------------
 id           | integer                |           | not null | nextval('variable_id_seq'::regclass)
 key          | character varying(250) |           |          | 
 val          | text                   |           |          | 
 is_encrypted | boolean                |           |          | 
 description  | text                   |           |          | 
Indexes:
    "variable_pkey" PRIMARY KEY, btree (id)
    "variable_key_key" UNIQUE CONSTRAINT, btree (key)
```

```
# listar variables
$ airflow> SELECT * FROM variable;


#listar usuarios
$ airflow> SELECT * FROM ab_user;

```



## Comandos básicos Postgres
___

| | |
| -- | -- |
| \d    | Lista as tabelas contidas em sua base |
| \d    |  nome da tabela	Descreve todos os atributos da tabela e suas propriedades |
| \g    | Executa determinada query |
| \q    | Sai do console psql |
| \i    | /caminho/pasta/script.sql   Importar um script.sql |
| \timing -- | Inicia ou para  o cronômetro para atividades |
| \dT+ -—    | Lista os tipos de dados do PG com detalhes |
| \cd—- | Muda para outro diretório |
| \dt   | Lista tabelas |
| \di   | Lista indices |
| \ds   | Lista sequências |
| \dv   | Lista views |
| \dS   | Lista tabelas do sistema |
| \dn   | Lista esquemas |
| \dp   | Lista privilégios |
| \e    | Abre o editor vi com a última consulta |
| \o    | Inicia ou termina a criação de arquivo. Ex.: \o arquivo.sql |
| \?    | Ajuda geral dos comandos do psql |
| \h*   | Exibe ajuda de todos os comandos |
| \encoding | Exibe codificação atual |


