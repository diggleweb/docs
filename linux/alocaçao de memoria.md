# alocacão de memoria

Para determinar a ocupação da memória relacionada a um aplicativo, qualquer uma das métricas a seguir pode ser usada:

* Resident Set Size (RSS): número de páginas compartilhadas e não compartilhadas usadas pelo app.

* Proporcional Set Size (PSS): número de páginas não compartilhadas usadas pelo app e uma distribuição uniforme das páginas compartilhadas. Por exemplo, se três processos compartilham 3 MB, cada um deles recebe 1 MB em PSS.

* Unique Set Size (USS): número de páginas não compartilhadas usadas pelo app (páginas compartilhadas não estão incluídas).

## trocando e descartando páginas

kernel swap daemon(kswapd): Quando a memória física se torna escassa, o subsistema de gerenciamento de memória do Linux deve tentar liberar as páginas físicas. Esta tarefa cabe ao daemon de troca do kernel ( kswapd ).

O daemon de troca do kernel ( kswapd ) é iniciado pelo processo de inicialização do kernel no momento da inicialização e fica esperando que o cronômetro de troca do kernel expire periodicamente.

## memoria a longo do tempo

> $ cat /proc/[pid]/status

> $ cat /proc/$(pidof prometheus)/status
donde: PIDOF, fornece pid de um processo em execucão

omitir processo com PID 
> pidof -o $(pidof prometheus)

listar arquivos do processo
> ls -la /proc/$(pidof prometheus)/

memoria mapeada por arquivo
> cat /proc/$(pidof prometheus)/smaps

tarefas por processo
> ls -la /proc/$(pidof prometheus)/task/

ver os arquivos abertos no mac
> lsof -p [PID]

## limpando memoria

```shell
# eliminando temporarios
rm -fr /tmp/android-alertrack/*

# remove arquivos cache.img
ls -ltr |grep 'cache.img'|awk '{print $9;}'|xargs rm -v

# Limpar cache, dentries e inodes.
sync; echo 3 > /proc/sys/vm/drop_caches



# reiniciar canal

```

## ferramentas

### Benchmarking de memória

### Examinando o uso da memória em todo o sistema

**vmstat** é uma das ferramentas de desempenho mais onipresentes. Há uma regra fundamental sobre vmstat , que você deve aprender e nunca esquecer: vmstat tenta apresentar uma média desde a inicialização na primeira linha. A primeira linha da saída do vmstat é totalmente lixo e deve ser descartada.

> vmstat 5
donde:
- swap: A quantidade de espaço de troca disponível, em KB.
- free: A quantidade de memória livre (ou seja, o tamanho da lista livre) em KB
- re: O número de páginas recuperadas da lista livre

### Examinando o uso de processos de memória

O espaço de endereço de cada processo, que é composto de muitos segmentos, pode ser medido das seguintes maneiras:

* O tamanho total do espaço de endereço do processo (representado por SZ ou SIZE)

* O tamanho residente (o tamanho da parte do espaço de endereço que é mantido na memória) do espaço de endereço do processo (RSS)

* O espaço de endereçamento compartilhado total

* O espaço de endereço privado total

> $ pmap -x <PID>

> $ ps uax | grep <process_name>

> $ cat /proc/[PID]/status

## install android for test

listar avds
> $ `~/Library/Android/sdk/emulator/emulator -list-avds`

path emulator and avd
> $ nano .zsh
export PATH=$PATH:~/.android-sdk-macosx/platform-tools/

export PATH="~/Library/Android/sdk/emulator:$PATH"

or
> echo -n 'export PATH=~/Library/Android/sdk/emulator:$PATH' >> ~/.zshrc

> $ source ~/.zshrc

## kvm

verificar a capacidade de execução de KVM
> grep -cw ".*\(vmx\|svm\).*" /proc/cpuinfo

> egrep -c '(vmx|svm)' /proc/cpuinfo

## init emulator

path
>  ~/.android/avd/

listar avds
> emulator -list-avds or $ `~/Library/Android/sdk/emulator/emulator -list-avds`

init
> emulator @Pixel_2_API_30

or 
> emulator @Pixel_3a_API_30_x86

verificar no top
> top -o cpu -stats pid,user,state,command,cpu,vsize,rsize,time

## scrip para limpar cache RAM diariamente as 2h por medio do cron

clearcache.sh
```shell
#!/bin/bash
# Note, we are using "echo 3", but it is not recommended in production instead use "echo 1"
echo "echo 3 > /proc/sys/vm/drop_caches"
```

> $ chmod 755 clearcache.sh

ativando o crontab
> crontab -e

`0  2  *  *  *  /path/to/clearcache.sh`

## Limpar espao de troca linux (kswapd)

> swapoff -a && swapon -a

```shell
#!/bin/bash
echo 3 > /proc/sys/vm/drop_caches && swapoff -a && swapon -a && printf '\n%s\n' 'Ram-cache and Swap Cleared'
```
or
> $ su -c "echo 3 >'/proc/sys/vm/drop_caches' && swapoff -a && swapon -a && printf '\n%s\n' 'Ram-cache and Swap Cleared'" root

toggle_swap.sh
```shell
#!/bin/bash

function echo_mem_stat () {
    mem_total="$(free | grep 'Mem:' | awk '{print $2}')"
    free_mem="$(free | grep 'Mem:'  | awk '{print $7}')"
    mem_percentage=$(($free_mem * 100 / $mem_total))
    swap_total="$(free | grep 'Swap:' | awk '{print $2}')"
    used_swap="$(free | grep 'Swap:' | awk '{print $3}')"
    swap_percentage=$(($used_swap * 100 / $swap_total))

    echo -e "Free memory:\t$((free_mem / 1024))/$((mem_total / 1024)) MB\t($mem_percentage%)"
    echo -e "Used swap:\t$((used_swap / 1024))/$((swap_total / 1024)) MB\t($swap_percentage%)"
}

echo "Testing..."
echo_mem_stat

if [[ $used_swap -eq 0 ]]; then
    echo "No swap is in use."
elif [[ $used_swap -lt $free_mem ]]; then
    echo "Freeing swap..."

    swapoff -a
    swapon -a

    echo_mem_stat
else
    echo "Not enough free memory. Exiting."
    exit 1
fi
```

## path of swap memory

> cat /proc/swaps

> grep swap /etc/fstab

## bibliografía

* alocação de memoria [link](https://developer.android.com/topic/performance/memory-overview)

* depuracao e uso de memoria android [link](https://perfetto.dev/docs/case-studies/memory)

* administrando memoria [link](https://developer.android.com/topic/performance/memory-management)

* iniciar emulator pela linha de comando [link](https://developer.android.com/studio/run/emulator-commandline)

* sysctl [link](https://www.kernel.org/doc/Documentation/sysctl/vm.txt)

* kernel analisys [link](https://tldp.org/HOWTO/KernelAnalysis-HOWTO-7.html) | [link 2](https://tldp.org/HOWTO/From-PowerUp-To-Bash-Prompt-HOWTO-8.html)

* memory [link](https://tldp.org/LDP/tlk/mm/memory.html)

* como liberar swap [link](https://askubuntu.com/questions/1357/how-to-empty-swap-if-there-is-free-ram)

* troubleshoot linux memory [link](https://upcloud.com/community/tutorials/troubleshoot-linux-memory-issues/)

* oom killer [link](https://www.oracle.com/technical-resources/articles/it-infrastructure/dev-oom-killer.html)

* out of memory killer [link](https://www.percona.com/blog/2019/08/02/out-of-memory-killer-or-savior/)

* performance tunning linux [link](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/performance_tuning_guide/sect-red_hat_enterprise_linux-performance_tuning_guide-configuration_tools-configuring_system_memory_capacity)
