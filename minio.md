# MINio

## Install minio into docker

> docker run -d -p 9000:9000 -p 9001:9001 -v "$PWD/datalake:/data" minio/minio server /data --console-address ":9001"

Abra o browser e digite: [http://localhost:9001/login](http://localhost:9001/login)

**username**: minioadmin
**password**: minioadmin

## configurando o datalake

- criar bucket [menu/muckets]
    - [bucket] landing: 
        - [pasta] performance-evaluation
        - [pasta] workings-hours

    - [bucket] processing: 

    - [bucket] curated: 