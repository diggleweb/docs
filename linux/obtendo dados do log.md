# obtendo dados do log
tail -f /var/log/zabbix/zabbix_agentd.log

# version do zabbix-agent and server
zabbix_agentd -V
zabbix_server -V

# parametros de configuracao
cat zabbix_agentd.conf | grep ^[A-Za-z]

# verificando procesos de zabbix
ps -eaf | grep zabbix

# verificando configuracao do agente
zabbix_agentd -c /etc/zabbix/zabbix_agentd.conf

# zabbix get ip porta
zabbix_get -s 192.168.0.188 -p 10050 -k "login_user"
zabbix_get -s 127.0.0.1 -p 10050 -k system.cpu.load[all,avg1]
zabbix_get -s 127.0.0.1 -p 10050 -k mysql.ping[127.0.0.1,3306]

# buscando texto e print em tela
grep -A10 -B10 Pid /etc/zabbix/zabbix_agentd.conf
cat /var/run/zabbix/zabbix_agentd.pid
cd /var/lib/zabbix/.my.cnf

# verificar log do zabbix server
cat /var/log/zabbix/zabbix_server.log | grep database

# pasta para senhas zabbix
cd  

# selinux
sealert -a /var/log/audit/audit.log
Ligue auditoria completa
auditctl -w /etc/shadow -p w

# O SELinux está impedindo que o /usr/sbin/php-fpm acesse o map no arquivo /var/lib/phpmyadmin/tmp/twig/77/77329f9a956af6a70502d4c8d97c2b02b2b40ec3768924c9e3b06a24b5eb5dfb.php.

setsebool -P domain_can_mmap_files 1

ausearch -c 'php-fpm'--raw | audit2allow -M my-phpfpm # semodule -X 300 -i my-phpfpm.pp

# O SELinux está impedindo que o /usr/sbin/php-fpm acesse o name_connect no tcp_socket port 443.
fa
## Se você quiser allow httpd to can network connect
setsebool -P httpd_can_network_connect 1

ausearch -c 'php-fpm'--raw | audit2allow -M my-phpfpm # semodule -X 300 -i my-phpfpm.pp

# O SELinux está impedindo que o /usr/sbin/zabbix_agentd acesse o name_connect no tcp_socket port 32774.

## Se você quiser allow nis to enabled
setsebool -P nis_enabled 1

# O SELinux está impedindo que o /usr/sbin/zabbix_server_mysql acesse o connectto no unix_stream_socket /run/zabbix/zabbix_server_lld.sock.
 ## Se você quiser allow daemons to enable cluster mode

 setsebool -P daemons_enable_cluster_mode 1

# O SELinux está impedindo que o /usr/sbin/php-fpm acesse o name_connect no tcp_socket port 10051.
## Se você quiser allow httpd to can network connect
setsebool -P httpd_can_network_connect 1

# O SELinux está impedindo que o /usr/bin/bash acesse o execute no arquivo /usr/bin/rpm.
permitir este acesso por agora executando: # ausearch -c 'sh'--raw | audit2allow -M my-sh # semodule -X 300 -i my-sh.pp

ausearch -c 'rpm'--raw | audit2allow -M my-rpm # semodule -X 300 -i my-rpm.pp

# estao inovando em:
- nivel de satisfaccao
- experiencia nos locais de consumo

# o que as empresas querem?
- ideias no obias
