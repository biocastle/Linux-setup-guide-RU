# Оптимизация Linux
### Ядро

Скомпилируем оптимизированное ядро, будем использовать скрипт [linux-tkg](https://github.com/Frogging-Family/linux-tkg) для установки, патча и компиляции ядра.
Также можно взять ядро от [CachyOS](https://github.com/CachyOS/linux-cachyos).


### Параметры GRUB

Изменять параметры grub можно открыв /etc/default/grub с помощью любого текстового редактора с привелегиями рута (администратора).
Нас интересует GRUB_CMDLINE_LINUX_DEFAULT и вписываем туда quiet splash nowatchdog mitigations=off raid=noautodetect pci=pcie_bus_perf


### Демоны

Ananicy-cpp - Демон, предназначенный для автоматической настройки приоритета.
Параметры в grub, компиляция ядра, планировщики задач (bore, EEVDF)


### ZRAM / ZSWAP
...

### Настройка частот CPU

##### Политики масштабирования частоты

Простым языков - планы электропитания
В Linux их существует много, примеры: performance, powersave, userspace, ondemand, conservative, schedutil

Каждая политика меняет работу CPU (изменение частот и т.д)

##### Драйверы масштабирования
Процессоры AMD и Intel могу сам выставлять себе частоту на основе данных от CPPC (Collaborative Processor Performance Control), с которыми процессор понимает какие выставлять частоты в данный момент. Для этого создали драйвера amd-pstate и intel-pstate

Режимы работы драйверов pstate:
*active* - обычно стоит по умолчанию в драйверах pstate,
*passive* - 
*guided* - тоже самое что и active, но может устанавливать минимальные и максимальные лимиты частоты CPU

Чтобы иметь возможность менять политики:

1) Открываем кофинг grub (по умолчанию - /etc/default/grub)
2) Находим строку GRUB_CMDLINE_LINUX_DEFAULT и в конец добавляем следущие параметры:
**Для AMD CPU:**
acpi_cpufreq amd_pstate=guided

**Для INTEL CPU:**
acpi_cpufreq intel_pstate=guided

Скачиваем программу cpupower (также подойдут и другие программы)
 (Arch Linux: pacman -S cpupower)

Теперь мы можем задавать CPU на каких частотах ему работать

Примеры:
sudo cpupower frequency-set -g performance

sudo cpupower frequency-set --min 4GHZ
