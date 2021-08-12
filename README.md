# cat-readme
Main link & BIG THX!!!!
https://github.com/ARM-software/u-boot/blob/master/board/qualcomm/dragonboard820c/readme.txt

## Nokia 6.1(Qualcomm Snapdragon 630) U-Boot
CPU: ARM Cortex-A53
GPU: Adreno 508
modem: X12 LTE(??)
RAM: 4 GB
ROM: 64 GB
## https://www.qualcomm.com/products/snapdragon-630-mobile-platform

Пчему создан данный репозиторий - пушто нефиг баловаться с EDL на нокии.
Вторая причина существования данной фигни - интерес возможности "нативного запуска и работы"..дааа нативного, если убили до такой же степени аппарат как я о_О

1) Надо достать загрузчик, самый простой это U-BOOT(Das U-BOOT). Подробнее на http://www.denx.de/wiki/U-Boot/WebHome
2) После загрузки надо законфигурировать загрузчик и собрать в кучку, параллельно думать про ос, которая будет установлена вместо штатного Ведроида(предположительно Арч, любой из дебианов, крайне маловероятно Гента, более вероятно - пересобранный андроид(взаимоисключающие параграфы ^___^)
3) После сборки всего всего, надо переразметить файл разметки(шта?!) и залить через QDL(ага, да) весь этот стафф на аппарат и пробовать загрузиться(наличие бэктрекинга в системе и загрузчике можно заранее предусмотреть)
4) Возможный профит(90% - что не будет) от другой операционной системы.

Третья причина(а наху..зачем?) - посмотреть, попробовать, оценить и подтянуть навыки в работе с такими с железками и наблюдать как будут работать данные операционные системы(скорее всего выберется какая-то одна).
Четвёртая причина - Just 4 lulz

Вообщем-то "как какать?":

1) Тащим сам Das U-BOOT
      
      ftp://ftp.denx.de/pub/u-boot/u
      
      wget ftp://ftp.denx.de/pub/u-boot/u-boot-1.3.2.tar.bz2

2) Данный загрузчик будет компилироваться на Debian-base дистрибутиве. Поэтому необходимо подготовить недостающие компоненты и обновить "старые".

2.1) Для начала:

      root# apt update && apt upgrade 

Это избавит от некоторых проблем с компиляторами и библиотеками, если они достаточно "старые".

2.2) Распаковать архив u-boot в какое-нибудь место на жёстком диске, разделе, как Вы это называете(?).

2.3) Понадобится "пакет" ccache. 

      root# apt reinstall ccache

Так же понадобится кросс-компилятор для arm64

      root# apt search gcc-aarch64-linux-gnu
      root# apt install gcc-aarch64-linux-gnu

И библиотека libfdt(в моём случае dev)
     
     root# install libfdt-dev

2.4) Так же с git необходимо "стянуть" skales. Рекомендуется это сделать в распакованный u-boot, но соль-перец по-вкусу.

     user[./uboot]$ git clone git://codeaurora.org/quic/kernel/skales

Стоит обратить ВНИМАНИЕ на то что существуют как минимум два источника skales:
1 - git://codeaurora.org/quic/kernel/skales в нём точно присутствует dtbTool mkbootimg
2 - git://source.codeaurora.org/quic/kernel/skales в нём присутствует только mkbootimg

2.5) Подготовка в принципе завершена. Вроде бы

3) Сам процесс компиляции зависит от доступных мощностей вашего устройства на котором это будете производить.

3.1) Находясь в папке u-boot

     user[./uboot]$ make mrproper
     user[./uboot]$ make distclean
     
Очистит от предыдущей конфигурации.

3.2) "Автоматическая генерация"(дегенерация..) файла .config для последующей сборки

     user[./uboot]$  CROSS_COMPILE="ccache aarch64-linux-gnu-" make dragonboard820c_config

Так же допускается использование "O=/.../"(Это буква О, а не ноль) для того чтобы билд лежал отдельно от всего остального.

3.3) Сама генерация

      user[./uboot]$ CROSS_COMPILE="ccache aarch64-linux-gnu-" make
      
      user[./uboot]$ touch rd
      user[./uboot]$ CROSS_COMPILE="ccache aarch64-linux-gnu-" ./dtbTool -o dt.img arch/arm/dts
      user[./uboot]$ CROSS_COMPILE="ccache aarch64-linux-gnu-" ./dtbTool -o dt.img build/arch/arm/dts
      user[./uboot]$ CROSS_COMPILE="ccache aarch64-linux-gnu-" ./mkbootimg --kernel=u-boot-dtb.bin --output=u-boot.img --dt=dt.img --pagesize 4096 --base 0x80000000 --ramdisk=rd --cmdline=""
      
4) По итогу получим img образ для того чтобы с него загрузиться или уже залить в качестве загрузчика в память устройства.

   $ fastboot boot u-boot.img

   or flash it to the UFS drive boot partition:

   $ fastboot flash boot u-boot.img
   $ fastboot reboot


Так же данная инструкция доступна из архива сырца загрузчика u-boot/board/qualcomm/dragonboard820c/readme.txt
