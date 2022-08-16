# Particionamento

# Sumário

# Partição de +2TB

Normalmente utilizamos o comando `fdisk` para formatar uma partição no link, podem ela não possui suporte para partições com mais de 2TB. Como nossos nós vão ter uma partição de 12TB é necessário utilizar outro recurso.

Nestes casos, utilizamos o comando `parted`  para criar a partição utilizando 100% do seu espaço disponível.

Para particionar corretamente, siga os passos abaixo:

```bash
# identifica a partição
lsblk

# inicia o particionamento usando o diretório da partição
parted /dev/sdc

# cria a etiqueta GPT
(parted) mklabel gpt

# define a unidade que a maquina vai tratar (TB)
(parted) unit TB

# cria partição primária (mínimo - máximo)
(parted) mkpart primary 0.00TB 4.80TB

# exibe o particionamento realizado
(parted) print

# sai do console do parted
(parted) quit

# formata a partição
mkfs.ext4 /dev/sdc1

# montar partição
mount /dev/sdc1 /mnt/mysql
```

<aside>
⚠️ **IMPORTANTE**
Aós definir a partição é necessário alterar o arquivo /etc/fstab para que ao boot o SO monte a partição desejada em `/etc/fstab`

Ex:
/dev/sdc1	  /mnt/mysql	  ext4	defaults   0  0

</aside>

## Particionamento de HD

o comando para particionar graficamente no shell de linux

> **lsblk**

> $ **sudo cfdisk**

```
Disk: /dev/sda
              Size: 1,9 TiB, 1199638052864 bytes, 2343043072 sectors
           Label: gpt, identifier: 3988391A-2F50-4862-BF9A-8DFEE22DF887

    Device         Start         End              Sectors           Size Type
>>  /dev/sda1      2048          4095              2048             1M BIOS boot                
    /dev/sda2      4096          3149823           3145728          1,5G Linux filesystem
    /dev/sda3      3149824       422580223         419430400        1,1T Linux filesyst
```

escolha a partição /dev/sda3 para redimensionar , ao dar resize ele criara nova particao /dev/sda4
```s
# formata a partição
mkfs.ext4 /dev/sda4

# montar partição
mount /dev/sda4 /home

# adicione no /etc/fstab para ser reconhecido ao reiniciar server
/dev/sda4	  /home	  ext4	defaults   0  0
```