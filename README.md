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

ой нунах кто будет читать это?! О_____о
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
https://ftp.denx.de/pub/eldk/5.6/
