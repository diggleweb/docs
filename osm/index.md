# Referencias: OpenStreetMap

# OpenStreetMap (OSM)

O OpenStreetMap, também conhecido como OSM, é um banco de dados do mapa-múndi (dados brutos) de contribuição do usuário que pode ser editado gratuitamente. Esses dados são então processados pelo **servidor de blocos** gerando blocos que são renderizados e servidos ao cliente.

**Pré-requisitos/Requisitos de Hardware**

• Todo o mapa do planeta requer pelo menos 32 G de RAM e disco SSD de 1 TB. Não é viável usar um disco rígido giratório para todo o mapa do planeta.

• O mapa do brazil requer pelo menos 15 G de RAM e 60 GB de espaço em disco. [[link](http://download.geofabrik.de/south-america.html)]

o mapa esta disponible na regiao: south Americana, sub-região: Brazil, .osm.pbf (1.4GB)

| sub-region | .osm.pbf |
| --- | --- |
| centro-oeste | (105 MB) |
| nordeste | (284 MB) |
| norte | (96 MB) |
| sudeste | (668 MB) |
| sul | (294 MB) |

mapa de país/estado/província/cidade individual, vá para  [http://download.geofabrik.de](http://download.geofabrik.de/)

ou [BBBike.org](http://download.bbbike.org/osm/) fornece extratos em diferentes formatos.

### Dependencias ****Open Street Map Tile Server(****servidor de blocos OSM)

- [PostgreSQL](https://www.postgresql.org/)
    
    - Banco de dados relacional de código aberto no qual os dados do mapa OSM serão importados.
    
- [PostGIS](http://postgis.net/)
    
    - Extensor de banco de dados espacial para PostgreSQL que suporta objetos geográficos e consultas de localização em SQL.
    
- [osm2pgsql](http://wiki.openstreetmap.org/wiki/Osm2pgsql)
    
    - Converte dados Open Street Map para bancos de dados PostgreSQL habilitados para PostGIS.
    
- [Mapnik](http://mapnik.org/)
    
    - Biblioteca de visualização e processamento geoespacial que renderiza blocos.
    
- [Apache HTTP Server](https://httpd.apache.org/)
    
    - Open servidor HTTP fonte conformidade com os padrões de HTTP.
    
- [mod_tile](https://github.com/openstreetmap/mod_tile)
    
    - Programa para renderizar (e rerenderizar) e servir blocos de mapa usando o Apache HTTP Server e o Mapnik como backend de renderização.
    
- [Render](http://wiki.openstreetmap.org/wiki/Mod_tile#renderd)
    
    - Sistema de filas prioritário para pedidos de renderização.
    
- [Boost C++](http://www.boost.org/)
    
    - Bibliotecas de origem C++ portáteis.
    
- [GEOS C++](https://trac.osgeo.org/geos/)
    
    - Mecanismo de geometria de código aberto para C++.
    
- [HarfBuzz](https://www.freedesktop.org/wiki/Software/HarfBuzz/)
    
    - Biblioteca de modelagem de texto para converter texto Unicode em índices e posições de glifos.
    
- [Carto](https://github.com/mapbox/carto/)
    
    - Linguagem de estilo de mapa semelhante a CSS que permite editar o estilo de mapas, incluindo formas, polígonos, fontes e cores.
    
- [OSM Carto](https://github.com/gravitystorm/openstreetmap-carto)
    
    - Folha de estilo Carto de código aberto para a camada de mapa padrão para mapas baseados em Open Street Map.
    
- [OSM Bright](https://github.com/mapbox/osm-bright)
    
    - Folha de estilo Carto de código aberto para criar mapas baseados em Open Street Map usando Mapnik.
    

# Nominatim

ferramenta para pesquisar dados OSM por nome e endereço e gerar endereços sintéticos de pontos OSM (geocodificação reversa).

Arquitectura basica:

- importação de dados
- cálculo do endereço
- frontend de busca.

[Intalação de nominatim in CentOS 7](https://nominatim.org/release-docs/latest/appendix/Install-on-Centos-7/)

# Projeto OSRM (****Open Source Routing Machine****)

Mecanismo de roteamento de alto desempenho escrito em C++ 14 projetado para rodar em dados OpenStreetMap. osrm tem os seguintes serviços:

- Nearest - Encaixa as coordenadas na rede de ruas e retorna as correspondências mais próximas
- Route - Encontra a rota mais rápida entre as coordenadas
- Table - Calcula a duração ou distâncias da rota mais rápida entre todos os pares de coordenadas fornecidas
- Match - Encaixa traços de GPS barulhentos na rede rodoviária da maneira mais plausível
- Trip - Resolve o problema do caixeiro viajante usando uma heurística gananciosa
- Tile - Gera Mapbox Vector Tiles com metadados de roteamento interno

[documentação](http://project-osrm.org/docs/v5.24.0/api/#)

****osrm/osrm-backend [****[https://github.com/Project-OSRM/osrm-backend](https://github.com/Project-OSRM/osrm-backend)****]****

****osrm/osrm-frontend [****[https://github.com/Project-OSRM/osrm-frontend](https://github.com/Project-OSRM/osrm-frontend)****]****

___
# preparando server para instalar docker docker-compose

```shell
# criar novo usuario para projeto osm 
$adduser osm
$passwd osm

# preparando o alma, eliminar o podman que ja vem no alma
$ yum remove buildah skopeo podman containers-common atomic-registries docker container-tools
$ rm -rf /etc/containers/* /var/lib/containers/* /etc/docker /etc/subuid* /etc/subgid*
$ cd ~ && rm -rf /.local/share/containers/

# atualizar alma e instalar ou verificar repositorios, docker
$ yum update -y
$ yum install curl dnf git wget -y
$ dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo
$ yum install docker-ce-cli containerd.io -y
$ yum install docker-ce -y
$ firewall-cmd --zone=public --add-masquerade --permanent
$ firewall-cmd --reload

# iniciar e ativar docker como serviço
$ systemctl start docker
$ systemctl status docker
$ systemctl enable docker
$ docker -v

# download docker-composer na pasta: `/usr/bin/docker-compose` para ser iniciado
$ curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose
$ chmod +x /usr/bin/docker-compose
$ docker-compose -v
```

## comandos docker

- download maps do brasil:
`wget -c http://download.geofabrik.de/south-america/brazil-latest.osm.pbf`


```shell
docker run -t -v "${PWD}:/data" osrm/osrm-backend osrm-extract -p /opt/car.lua /data/brazil-latest.osm.pbf
docker run -t -v "${PWD}:/data" osrm/osrm-backend osrm-partition /data/brazil-latest.osrm
docker run -t -v "${PWD}:/data" osrm/osrm-backend osrm-customize /data/brazil-latest.osrm
docker run -t -i -p 5000:5000 -v "${PWD}:/data" osrm/osrm-backend osrm-routed --algorithm mld /data/brazil-latest.osrm

# frontend
docker run -p 9966:9966 osrm/osrm-frontend xdg-open 'http://127.0.0.1:9966'
```

## Nominatim

### Option 1

```yml
# https://github.com/bringnow/docker-nominatim
version: '2.1'
services:
  nominatim:
    image: bringnow/nominatim
    volumes:
      - ${IMPORT_DATA_DIR:-./volumes/importdata}:/importdata
    environment:
      - PGHOST=postgis
      - PLANET_DATA_URL=${PLANET_DATA_URL:-http://download.geofabrik.de/europe/monaco-latest.osm.pbf}
      - OSM2PGSQL_CACHE=${OSM2PGSQL_CACHE:-14000}
    ports:
      - ${EXTERNAL_PORT:-127.0.0.1:8080}:80
    restart: always
  postgis:
    image: mdillon/postgis:9.4
    environment:
      - POSTGRES_DB=nominatim
      - POSTGRES_USER=nominatim
      - POSTGRES_PASSWORD=nominatim
    volumes:
      - nominatim-database:/var/lib/postgresql/data
      - ./postgis/set-auth.sh:/docker-entrypoint-initdb.d/set-auth.sh
      - ./postgis/skip-initdb-postgis.sh:/docker-entrypoint-initdb.d/postgis.sh
      - ./postgis/tune-postgres.sh:/docker-entrypoint-initdb.d/tune-postgres.sh
    volumes_from:
      - nominatim:ro # Needed for the Nominatim PostgreSQL module
    restart: always
volumes:
  nominatim-database:
    external: true
```

### Option 2

```yml
# https://github.com/helvalius/nominatim-docker
```

### Option 3

``` shell
docker run -it --rm \
    -e PBF_URL=http://download.geofabrik.de/south-america/brazil-latest.osm.pbf \
    -e REPLICATION_URL=http://download.geofabrik.de/south-america/brazil-updates/ \
    -p 8080:8080 \
    --name nominatim \
    mediagis/nominatim:4.0
```

#### custom pbf

```shell
docker run -it --rm \
    -e PBF_PATH=/nominatim/data/brazil-latest.osm.pbf \
    -p 8080:8080 \
    -v /osm-maps/data:/nominatim/data \
    --name nominatim \
    mediagis/nominatim:4.0
```

```yml
# https://github.com/mediagis/nominatim-docker/tree/master/4.0
version: "3"

services:
    nominatim:
        container_name: nominatim
        image: mediagis/nominatim:4.0
        restart: always
        ports:
            - "8080:8080"
        environment:
            # see https://github.com/mediagis/nominatim-docker/tree/master/4.0#configuration for more options
            PBF_URL: /nominatim/data/brazil-latest.osm.pbf
            # REPLICATION_URL: https://download.geofabrik.de/europe/monaco-updates/
            NOMINATIM_PASSWORD: very_secure_password
        volumes:
            - ./data01:/usr/share/elasticsearch/data
            - nominatim-data:/var/lib/postgresql/12/main
        shm_size: 1gb

volumes:
    nominatim-data:

```

___

#### docker-compose

```yml
version: "3"
services:
  osrm:
    container_name: osrm
    image: osrm/osrm-backend
    restart: always
    ports:
      - 5000:5000
    volumes:
      - ./osrm:/data
    command: "osrm-routed --max-matching-size 1000 --max-table-size 1000 --max-viaroute-size 1000 --algorithm mld /data/brazil-latest.osrm"

  vroom:
    network_mode: host
    image: vroomvrp/vroom-docker:v1.11.0
    container_name: vroom
    volumes:
      - ./vroom-conf/:/conf
    environment:
      - VROOM_ROUTER=osrm  # router to use, osrm, valhalla or ors
    depends_on:
      - osrm


  # EXAMPLE for Valhalla, please consult the repo for details: https://github.com/gis-ops/docker-valhalla
#  valhalla:
#    image: gisops/valhalla:latest
#    container_name: valhalla_latest
#    ports:
#      - 8002:8002
#    build:
#      context: .
#     # in case you need to build image without requiring sudo privileges on the files created by the container, you should provide your user's UID/GID
#      args:
#        - VALHALLA_UID=1000
#        - VALHALLA_GID=1000
#    volumes:
#      - ./custom_files:/custom_files
#    environment:
#      # Auto-download PBFs from Geofabrik
#      - tile_urls=https://download.geofabrik.de/europe/andorra-latest.osm.pbf
#      - server_threads=2  # determines how many threads will be used to run the valhalla server
#      - use_tiles_ignore_pbf=True  # load existing valhalla_tiles.tar directly
#      - build_elevation=True  # build elevation with "True" or "Force": will download only the elevation for areas covered by the graph tiles
#      - build_admins=True  # build admins db with "True" or "Force"
#      - build_time_zones=True  # build timezone db with "True" or "Force"
#      - build_tar=True  # build an indexed tar file from the tile_dir for faster graph loading times
#      - force_rebuild=False  # forces a rebuild of the routing tiles with "True"

  # EXAMPLE for OpenRouteService, please consult the repo for details: https://github.com/GIScience/openrouteservice
#  ors:
#    container_name: ors
#    ports:
#      - 8080:8080
#    image: openrouteservice/openrouteservice:latest
#    volumes:
#      - ./graphs:/ors-core/data/graphs
#      - ./elevation_cache:/ors-core/data/elevation_cache
#      - ./logs/ors:/var/log/ors
#      - ./logs/tomcat:/usr/local/tomcat/logs
#      - ./conf:/ors-conf
#      - ./path/to/pbf:/ors-core/data/osm_file.pbf  # alter path to your local OSM PBF file, e.g. from https://download.geofabrik.de
#    environment:
#      - BUILD_GRAPHS=False  # Forces the container to rebuild the graphs, e.g. when PBF is changed in app.config
#      - "JAVA_OPTS=-Djava.awt.headless=true -server -XX:TargetSurvivorRatio=75 -XX:SurvivorRatio=64 -XX:MaxTenuringThreshold=3 -XX:+UseG1GC -XX:+ScavengeBeforeFullGC -XX:ParallelGCThreads=4 -Xms1g -Xmx2g"
#      - "CATALINA_OPTS=-Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9001 -Dcom.sun.management.jmxremote.rmi.port=9001 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false -Djava.rmi.server.hostname=localhost"
```

### Option 4


### Referencias Bibliográficas:

- [install openstreetmap in ubuntu server 18](https://www.linuxbabe.com/ubuntu/openstreetmap-tile-server-ubuntu-18-04-osm)
- [instal servidor de blocos in centOS7]()
- [osrm in docker](https://medium.com/@fbaierl1/setting-up-vroom-osrm-with-docker-compose-c8dc48d0cb2a)
- https://knowledgebase.hyperlearning.ai/en/articles/centos-7-open-street-map-tile-server
- http://project-osrm.org/docs/v5.24.0/api/#
- https://www.yatis.io/how-to-install-osrm-and-nominatim-on-ubuntu-16-02-google-maps-alternative/

