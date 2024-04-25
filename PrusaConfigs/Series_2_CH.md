# Печать с подогревом камеры

Для печати с подогревом включаем подогрев камеры в настрйоках принтера

И создаём отдельные профили в PrusaSlicer, изменяя Пользовательский G-code

### Стартовый g-code.

```
G21 ;dimensions in millimeters
G90 ;absolute coordinate system
M104 T0 S120 ; преднагрев сопла
M140 S{first_layer_bed_temperature[0]} ; преднагрев стола
M141 S80 ; преднагрев камеры
G28
G0 F600 X180 Y180 Z80
M190 S{first_layer_bed_temperature[0]} ; греем стол
M191 S80 ; греем камеру
M109 T0 S{first_layer_temperature[0]} ; греем сопло
```

Необходимая температура камеры задаётся командами M141/M191

Для маленьких принтеров температура ограничего 80 градусами, для больших - 90


Стартовый G-code
```
{if first_layer_bed_temperature[1]>first_layer_bed_temperature[0]}M190 S{first_layer_bed_temperature[0]}{else}M190 S{first_layer_bed_temperature[1]}{endif} ; сравниваем температуры стола
M109 T0 S{first_layer_temperature[0]}
M109 T1 S{first_layer_temperature[1]}
G28 ; home all axes
G1 Z5 F5000 ; lift nozzle
```