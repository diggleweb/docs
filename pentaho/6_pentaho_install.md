# Install pentaho in mac

## prerequisitos

- java version 1.8

    > brew install java

    > java -version

        ```
        java version "15.0.2" 2021-01-19
        Java(TM) SE Runtime Environment (build 15.0.2+7-27)
        Java HotSpot(TM) 64-Bit Server VM (build 15.0.2+7-27, mixed mode, sharing)
        ```
- verificar versões instaladas:
        
    > /usr/libexec/java_home -v

        ```
        15.0.2, x86_64:	"Java SE 15.0.2"	/Library/Java/JavaVirtualMachines/jdk-15.0.2.jdk/Contents/Home
        1.8.0_282, x86_64:	"AdoptOpenJDK 8"	/Library/Java/JavaVirtualMachines/adoptopenjdk-8.jdk/Contents/Home
        1.8.0_202, x86_64:	"Java SE 8"	/Library/Java/JavaVirtualMachines/jdk1.8.0_202.jdk/Contents/Home
        ```
        
- exportar no zsh

        ```
        export JAVA_HOME=$(/usr/libexec/java_home -v 15.0.2)
        export JAVA_HOME=$(/usr/libexec/java_home -v 1.8.0_202)
        export JAVA_HOME=$(/usr/libexec/java_home -v 1.8.0_202)
        ```
    > java -version

        ```
        java version "1.8.0_202"
        Java(TM) SE Runtime Environment (build 1.8.0_202-b08)
        Java HotSpot(TM) 64-Bit Server VM (build 25.202-b08, mixed mode)
        ```

* Passo 1: Download the community edition of pentaho

* Passo 2: Extrack and unzip an copy paste `data-integration` into applications

    > cd /Applications/data-integration/Data Integration.app/Contents/MacOs

    > ./JavaApplicationStub

    - Se retornar o seguente erro:

        ```
        LSOpenURLsWithRole() failed with error -10810 for the file Data Integration.app
        ```
    correr o seguinte comando para inserir permisoes
    > sudo xattr -dr com.apple.quarantine Data\ Integration.app

* Passo 4: 

## configuracoes

- configure conection com mysql

    arquivo JNDI_mysql.text
    ```
    dwsucos/type=javax.sql.DataSource
    dwsucos/driver=com.mysql.jdbc.Driver
    dwsucos/url=jdbc:mysql://localhost:3306/dwsucos
    dwsucos/user=root
    dwsucos/password=root
    ```
    configure os dados de conecao com mysql no seguinte arquivo:
    edite o arquivo `/Applications/data-integration/simple-jndi/jdbc.properties`

- criando arquivos de variaveis
    path:
    > nano ~/.kettle/kettle.properties

    adicione a seguntes variaveis:
    ```
    # windows
    diretorio=c:\\treinamento\\arquivos\\

    # macos
    diretorio=~/Documents/treinamento/arquivos/
    diretorio=/Users/alexyucra/Documents/treinamento/arquivos/
    # db
    banco=dwsucos
    ```
- criando variable de sistema, aonde sera aberto na variable de ambiente usamos a variable `kettle_home`

    > export KETTLE_HOME=$(/<path>)

    ```
    kettle_home=
    ```

## Conecão do Pentaho com mysql no xamp

- download conector jdbc [link for download](https://dev.mysql.com/downloads/connector/j/)

    copie e cole o aquivo `mysql-connector-java-8.0.26.jar` nas pastas:
    - data-integration/lib
    - pentaho-server/tomcat/lib
    - report-designer/lib/jdbc
    - schema-workbench/lib


## Bibliografia

- [run pentaho if erro](https://andres.jaimes.net/1388/running-pentaho-spoon-on-mac-osx/)
- [how to install pentaho in mac](https://medium.com/@originaleye/how-to-install-pentaho-8-2-on-a-mac-4e4f8d526df2)

- [installing mysql jdbc drivers](http://holowczak.com/installing-mysql-jdbc-drivers-in-pentaho-data-integration-and-ba-server-tools/)
- [como criar conexao mysql no pentaho](http://etlnapratica.blogspot.com/2016/07/como-criar-conexao-mysql-no-spoon.html)
- [documentacao pentaho](https://help.hitachivantara.com/Documentation/Pentaho/7.1/0H0/Specify_Data_Connections_for_the_Pentaho_Server/Define_Data_Connections_for_the_Pentaho_Server)


