<mark style="background: #FFB86CA6;">OSA-CM-Navigation-Component</mark> далее просто компонент является источником навигационной информации для АРМ-К.
Взаимодействие с компонентом происходит через <mark style="background: #FFB86CA6;">OSA-CM-Navigation-API</mark> далее просто апи.
Компонент поддерживает выбор источника навигационной информации для положения и для ориентации.
Поддерживаемые типы источников навигационной информации:
- бинс
- вручную

Компонент напрямую с бинс не работает, <mark style="background: #ADCCFFA6;">взаимодействие с бинс происходи через буарм</mark>.
На текущий момент <mark style="background: #ADCCFFA6;">компонент только слушает буарм</mark> для получения навигационной информации (положение, ориентация в пространстве) от бинс.
[Ссылка на протокол](https://repo.okbtsp.com/projects/BUMBLEBEE/repos/interface/browse/LanKsa/AboxArmkBinsControl.h)

Когда ориентация задана вручную (т.е. источников навигационной информации для ориентации: вручную), <mark style="background: #ADCCFFA6;">компонент отправляет значения углов на буарм</mark>.
[Ссылка на протокол](https://repo.okbtsp.com/projects/BUMBLEBEE/repos/interface/browse/LanSscSvrSrp/ArmkManualSinsAngles.h)

![[Navigation Description Diagramm.png]]

