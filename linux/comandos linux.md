# comandos linux

## monitorar o uso da memória do sistema

$ free -m    # (-m megabits, -g gigabits, -h modo humano) 
$ lscpu      # informacoes do sistema
$ ulimit -a # verifica limites maximos do servidor (kbytes, -m)
$ mysql --version
$ echo '\s' | mysql

### memoria_maxima_suportada RAM por slot

$ dmidecode -t 16
    - Maximum Capacity: 6 TB
    - Number Of Devices: 96
$ dmidecode -t 16 | grep Maximum
### memoria atual RAM

$ dmidecode -t 17

### mapa de RAM

$ dmidecode -t memory | sed -ne '/Memory Device/,/Part Number/ { /Size:/h; /^[[:space:]]*Locator:/ {p;x;p}; /Speed:/p}' | paste - - - | tr -s '\t' | expand -t 1,20,50

### mostrar final de um arquivo

exemp
$ sudo tail -f /var/log/syslog

### listar modulos cargados em memoria

$ lsmod # lista modulos

$ rmmod # descarga modulos

### Exibe informações em tempo real sobre a memória cache

$ sudo slabtop

### Exibe estatísticas sobre a memória virtual

[vmstat](https://guialinux.uniriotec.br/vmstat/)

$ watch vmstat

$ watch 'ls -lh /<dir>/*.*'

$ watch 'du -sh *.*'

### vigiar tamanho e mudanzas no directorio

> $ `watch -d -n 1 'du --max-depth=5 "/tmp" | sort -r -k1,1n'`

a onde:
```s
watch: executa o mesmo comando periodicamente
options:
-d destaca as diferenças durante as execuçÕes
-n 1 é para atualizar a cada 1 segundo

du: verifica tamanho dos diretorios
options:
--max-depth=5 é até quantos níveis você quer apresentar no resultado
/tmp é o diretório que você deseja monitorar

sort: ordena resultado
options:
-r -k1,1n organiza em ordem numérica decrescente
```

> $ for i in `ps -eaf | grep alertrack | grep -v grep | awk '{print $2}'`; do echo -n "PID $i actual memory usage is :" >> totaluse.txt; pmap -d $i | grep -i "writeable/private: " >> totaluse.txt; done

___
fornece a soma de todos os valores "graváveis ​​/ privados" sem envolver nenhum arquivo. Claro que você pode estender a alternativa "grep | awk | tail" para a forma completa, no caso de algum outro grep / awk / tail estar usando sua memória ao mesmo tempo.

> $ echo| for i in `ps aux | grep -vE 'grep|awk|tail|$BASHPID' | awk '{print $2}' | tail -n +2`; do pmap -d $i | tail -1 | tr -s ' ' | cut -d ' ' -f4 | sed 's/K$//'; done | awk '{ sum += $1 } END { print sum" KB // " sum/1024" MB // " sum/1024/1024" GB" }'

```s
4099540 KB // 4003.46 MB // 3.90963 GB
```
___



copia de dados
$ cp userdata-qemu.img.qcow2 userdata-qemu.img.qcow2.bak

top
> top -c -u alertrack
> top -c -u alertrack

porcentagem de memoria usada
$ free -m | grep Mem | awk '{print $3/$2 * 100.0}'

porcentagem de memoria livre
$ free -m | grep Mem | awk '{print $4/$2 * 100.0}'

$ smem -tw
```s
Area                           Used      Cache   Noncache 
firmware/hardware                 0          0          0 
kernel image                      0          0          0 
kernel dynamic memory        754932     420612     334320 
userspace memory             964768      73480     891288 
free memory                  162372     162372          0 
----------------------------------------------------------
                            1882072     656464    1225608 
```
## verificar htop

Memória total usada = MemTotal-MemFree
Memória sem cache / buffer (verde) = Memória total usada - (Buffers + memória em cache)
Buffers (azul) = Buffers
Memória em cache (amarelo) = Cached+ SReclaimable-Shmem
Trocar = SwapTotal-SwapFree
___

> cat /proc/meminfo



```shell
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
 0  0      0 7024724   6016 890384    0    0     5    70   24   56 26 11 63  0  0
```

$ watch vmstat -S M -s

```shell
15933 M total memory
         8604 M used memory
         8447 M active memory
         2203 M inactive memory
         4919 M free memory
           26 M buffer memory
         2382 M swap cache
          976 M total swap
            0 M used swap
          976 M free swap
     17204009 non-nice user cpu ticks
          518 nice user cpu ticks
      6233776 system cpu ticks
     42423847 idle cpu ticks
       129032 IO-wait cpu ticks
            0 IRQ cpu ticks
      1311766 softirq cpu ticks
            0 stolen cpu ticks
      3535182 pages paged in
     48452309 pages paged out
            0 pages swapped in
            0 pages swapped out
    711424961 interrupts
   1298403474 CPU context switches
   1617718624 boot time
        68942 forks
```

### Limpar memoria virtual

1. Limpe o cache apenas

> $ `sync; echo 1 > /proc/sys/vm/drop_caches`

2. Limpar dentries e inodes:

> $ `sync; echo 2 > /proc/sys/vm/drop_caches`

3. Limpar cache, dentries e inodes.

> $ `sync; echo 3 > /proc/sys/vm/drop_caches`

### admin process

$ ps aux | grep alertrack | awk '{printf "%6s", $1} {printf "%9s  ",$2} {printf "%9s  ",$5} {printf "%9s  ",$6} {printf "\n"}'
___

## analise parametros de inicializaçao
ao inicializar nodo canal:
$ `emulator @shaw -writable-system -nocache -selinux -noaudio -no-boot-anim -gpu off`

na pasta /tmp/android-alertrack gera-se um sesaao com arquivos de contiguração:

du -h
```s
68K	./c6a9254f-bd5f-49bd-ab78-b92d773ff4d4
8,0K	./1287fb6e-589d-49f4-b8ab-3ecda7a4b9aa
24K	./dd5b3ea7-7918-4a89-9812-555d69b5908e
40K	./e0b4e52c-c445-4b57-b142-fefa85bd3157
148K	./539e1a63-ecc3-40cf-a761-233e85ed101cls
...
```
cada pasta contem txt de configuração

> $ `ls -la /tmp/android-alertrack/`
mostrara arquivos tmps que sao eliminados ao reiniciar canal, gerando novo pasta de sessao.du -h
  emulator-GrX6XC
  emulator-GrX6XC.qcow2












## Bibliografía

[Comandos linux](https://guialinux.uniriotec.br/)

[como liberar memoria RAM](https://kinglinux.xyz/2019/06/como-liberar-memoria-ram-em-servidores-gnu-linux.html)