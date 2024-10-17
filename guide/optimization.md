# Оптимизация Linux
Для начала скомпилируем оптимизированное ядро, будем использовать скрипт [linux-tkg](https://github.com/Frogging-Family/linux-tkg) для установки, патча и компиляции ядра.
Также можно взять ядро от [CachyOS](https://github.com/CachyOS/linux-cachyos).

Изменять параметры grub можно открыв /etc/default/grub с помощью любого текстового редактора с привелегиями рута (администратора).
Нас интересует GRUB_CMDLINE_LINUX_DEFAULT и вписываем туда quiet splash nowatchdog

Параметры в grub, компиляция ядра, планировщики задач (bore, EEVDF)
