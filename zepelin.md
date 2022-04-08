# install zepelin

[how to install](https://zeppelin.apache.org/docs/0.10.0/quickstart/install.html)

```shell
    docker run -u $(id -u) -p 8080:8085 --rm \
    -v $PWD/logs:/logs \
    -v $PWD/notebook:/notebook \
    -v /usr/lib/spark-2.4.7:/opt/spark \
    -v /usr/lib/flink-1.12.2:/opt/flink \
    -e FLINK_HOME=/opt/flink \
    -e SPARK_HOME=/opt/spark \
    -e ZEPPELIN_LOG_DIR='/logs' \
    -e ZEPPELIN_NOTEBOOK_DIR='/notebook' \
    --name zeppelin apache/zeppelin:0.10.0
```
