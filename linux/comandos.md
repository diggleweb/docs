# Comandos linux

## adicionar usuarios

listar usuarios linux
> $ `cat /etc/passwd`

> $ `adduser mynewuser` # new user

> $ `passwd mynewuser` # change password

> $ `sudo usermod -aG wheel <usuario>`
> $ `sudo usermod -a -G sudo <usuario>`

listar grupos



## Gerenciamento de partiões

> fdisk [opcao]

opcao:

    -b tamanho : especifica o tamanho do setor. São valores válidos: 512, 1024, 2048 or 4096. Usado apenas nas versões antigas do kernel.
    -C tamanho : especifica o número de cilindros do disco.
    -h : exibe informações sobre o fdisk.
    -l : lista as partições existentes no disco atual (caso o usuário não especifique o disco).
    -s partição : lista o tamanho da partição em blocos.
    -v : exibe versão do aplicativo.

```shell
$ sudo fdisk -l # listar particoes
$ sudo fdisk -l /dev/sda1 # ver particoes do /dev/sda1

```
[link](https://guialinux.uniriotec.br/fdisk/#:~:text=O%20comando%20df%20exibe%20informa%C3%A7%C3%B5es,discos%20SATA%2FIDE%20do%20sistema.)

## chek free disk space [link](https://opensource.com/article/18/7/how-check-free-disk-space-linux)

- **`df`** exibe informações sobre os espaços, livres e ocupados, das partições.
  - `df -h` mostra o espaço em disco em formato legível por humanos
  - `df -m` mostra o uso completo do disco do sistema de arquivos mesmo se o campo Disponível for 0
  - `df -T` mostra o uso do disco junto com o tipo de sistema de arquivos de cada bloco
  - `df -i` mostra inodes usados ​​e livres
  
- **`du`** exibe informações sobre o espaço usado pelos diretórios e arquivos.
  - `du -h` formato humano
  - `du -a` uso do disco para todos os arquivos
  - `du -s` espaco total em disco usado por um determinado arquivo
- **`fsck`** verifica e recupera sistemas de arquivos.
- **`hdparm`** exibe/altera os parâmetros de discos SATA/IDE do sistema.
- **`smartctl`** exibe relatório detalhado sobre os discos IDE/SCSI existentes no sistema.

usando opcoes:
- **`du | sort | head`**
- **`$  du | sort -nr | head -5`**, opcoes-sort: -n=numeric, -r=reverso
- **`$  du -h | sort -nr | head -5`**,
## Comando de status 

encontrar arquivos grandes:
- **`$ du -ah | sort -hr | head -5`**

`stat <file/directory>` exibe o tamanho e outras estatísticas de um arquivo/diretório ou um sistema de arquivos.

## erro: sort: write failed: /tmp/sortp2p3mn: No space left on device

- Essa diferença entre a saída de du -she df -hpode acontecer se algum arquivo grande tiver sido excluído, mas ainda estiver aberto por algum processo.

> lsof | grep deleted

> killall <process_name>

## check hd disk

- informacões do hd particões
- 
> lsblk -a
> lsblk -b

## filter with htop

> htop -p $(pgrep -d',' -f "android")
> 
## Bibliografia

- [sistema de particoes de um dispositivo](https://sempreupdate.com.br/como-listar-informacoes-de-dispositivos-discos-e-particoes-com-lsblk-no-linux/)
- [configurar servidor dns](https://tiparaleigo.wordpress.com/2020/01/06/como-configurar-o-servidor-dns-bind-no-centos-8-rhel8/)