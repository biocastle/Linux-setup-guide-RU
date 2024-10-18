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


# ZRAM / ZSWAP
...

# Настройка частот CPU
Открываем кофинг grub /etc/default/grub
Находим строку GRUB_CMDLINE_LINUX_DEFAULT и в конец добавляем следущие параметры:

**AMD CPU:**
"acpi_cpufreq amd_pstate=guided" (без ковычек)

**INTEL CPU:**
"acpi_cpufreq intel_pstate=guided" (без ковычек)

Скачиваем программу cpupower (Arch Linux: pacman -S cpupower)

Теперь мы можем задавать CPU на каких частотах ему работать

Примеры:
sudo cpupower frequency-set -g performance

sudo cpupower frequency-set --min 4GHZ
