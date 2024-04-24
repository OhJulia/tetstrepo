# Настройки для Series1

## Designer X

Максимальная высота печати 210 мм
Экструдеры 1
Тип g-code Marlin (legacy)
Включить функцию переменной высоты слоя - по желанию

Стартовый G-code
```
M190 S{first_layer_bed_temperature[0]}
M109 T0 S{first_layer_temperature[0]}
G28 ; home all axes
G1 Z5 F5000 ; lift nozzle
```
G-code выполняемый перед сменой слоя
```
M532 X0 L[layer_num] Z[layer_z]
```

