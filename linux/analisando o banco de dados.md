# analisando o banco de dados

como primero passo precisei acessar ao banco de dados,
abri as port 3306 para conceccion externa com o mysqlworkbench

# ativando schema de desempenho en /etc/mysql/my.cnf

performance_schema=ON
performance-schema-instrument='stage/%=ON'
performance-schema-consumer-events-stages-current=ON
performance-schema-consumer-events-stages-history=ON
performance-schema-consumer-events-stages-history-long=ON

> systemctl restart mariadb.service

# caminho do mariadb.log

/var/log/mariadb/mariadb.log

```s
2020-06-10 10:30:31 0 [Warning] mysqld: GSSAPI plugin : default principal 'mariadb/test-dba@' not found in keytab
2020-06-10 10:30:31 0 [ERROR] mysqld: Server GSSAPI error (major 851968, minor 2529639093) : gss_acquire_cred failed -Unspecified GSS failure.  Minor code may provide more information. Keytab FILE:/etc/krb5.keytab is nonexistent or empty.
2020-06-10 10:30:31 0 [ERROR] Plugin 'gssapi' init function returned error.
```

> mysql -u root -p
> SHOW ENGINES;
> SHOW ENGINE PERFORMANCE_SCHEMA STATUS;
> SHOW VARIABLES LIKE 'performance_schema';

# verificando version do mariadb com version do mysql-sys

MariaDB [sys]> SELECT @@version, plugin_name, plugin_auth_version
    ->   FROM information_schema.plugins WHERE plugin_name = 'PERFORMANCE_SCHEMA';
+-----------------+--------------------+---------------------+
| @@version       | plugin_name        | plugin_auth_version |
+-----------------+--------------------+---------------------+
| 10.4.13-MariaDB | PERFORMANCE_SCHEMA | 5.6.40              |
+-----------------+--------------------+---------------------+

MariaDB [sys]> SELECT * FROM sys.version;
+-------------+-----------------+
| sys_version | mysql_version   |
+-------------+-----------------+
| 1.5.2       | 10.4.13-MariaDB |
+-------------+-----------------+

ALTER DATABASE zabbixdb CHARACTER SET = utf8 COLLATE = utf8_general_ci;