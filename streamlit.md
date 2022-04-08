# how to install streamlit in CentOS

- create your app

- create user unto centos
    
    listar usuarios linux
    > $ `cat /etc/passwd`

    > $ `adduser mynewuser` # new user

    > $ `passwd mynewuser` # change password

- create `run.sh` file

    ```shell
        #!/usr/bin/env bash
        
        streamlit run app.py
    ```
    > chmod +x run.sh
    > ./run.sh

- Abrir portas do firewall
    > sudo firewall-cmd --zone=public --add-port=8501/tcp --permanent

    > sudo systemctl restart firewalld.service

    verificar portas:
    > firewall-cmd --list-all

- create streamlit como servico

    create file:
    > nano /lib/systemd/system/streamlit.service

    ```shell
    # service name:     streamlit.service
    # path:             /lib/systemd/system/streamlit.service

    [Unit]
    Description=Dashboard

    [Service]
    Type=simple
    PIDFile=/run/streamlit.pid

    User=streamlit
    Group=streamlit
    WorkingDirectory=/home/streamlit/dashboard/
    ExecStart=/home/streamlit/dashboard/run.sh --logging.dest="/var/log/streamlit/streamlit.log"
    
    Restart=on-failure
    RestartSec=10
    #KillMode=mixed

    [Install]
    WantedBy=multi-user.target
    ```

- run service
    
    > systemctl daemon-reload  

    > systemctl enable streamlit.service

    > systemctl start streamlit.service

    > systemctl status streamlit.service
