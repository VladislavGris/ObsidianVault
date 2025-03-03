## Пример структуры *VersionRequest.xml*:

```xml
<units>
  <unit id="2" name="Версии ПО AW-TDS" range="0">
    <operations>
      <operation access="0" id="21,22,23,201,205,215,218,219,221" name="Версии ПО" network="0" />
    </operations>
  </unit>
  <unit id="2" name="AW-TDS" range="0">
    <operations>
      <operation access="0" id="21" name="BBEE-AwsTds" network="0">
        <variables>
          <variable coeff="1" offset="0" size="32" type="git"></variable>
        </variables>
      </operation>
      <operation access="0" id="22" name="BBEE-MarkDetector" network="0">
        <variables>
          <variable coeff="1" offset="0" size="32" type="git"></variable>
        </variables>
      </operation>
      <operation access="0" id="23" name="BBEE-TargetProcessing" network="0">
        <variables>
          <variable coeff="1" offset="0" size="32" type="git"></variable>
        </variables>
      </operation>
      <operation access="0" id="201" name="FileManager" network="0">
        <variables>
          <variable coeff="1" offset="0" size="32" type="git"></variable>
        </variables>
      </operation>
      <operation access="0" id="205" name="FCAgent" network="0">
        <variables>
          <variable coeff="1" offset="0" size="32" type="git"></variable>
        </variables>
      </operation>
      <operation access="0" id="215" name="CommunicationRouter" network="0">
        <variables>
          <variable coeff="1" offset="0" size="32" type="git"></variable>
        </variables>
      </operation>
      <operation access="0" id="217" name="VideoWriter" network="0">
        <variables>
          <variable coeff="1" offset="0" size="32" type="git"></variable>
        </variables>
      </operation>
      <operation access="0" id="218" name="DocumCleaner" network="0">
        <variables>
          <variable coeff="1" offset="0" size="32" type="git"></variable>
        </variables>
      </operation>
      <operation access="0" id="219" name="VideoPlayer" network="0">
        <variables>
          <variable coeff="1" offset="0" size="32" type="git"></variable>
        </variables>
      </operation>
      <operation access="0" id="221" name="DocumWriter" network="0">
        <variables>
          <variable coeff="1" offset="0" size="32" type="git"></variable>
        </variables>
      </operation>
    </operations>
  </unit>
  <unit id="2" name="Версии ДОП ПО" range="0">
    <operations>
      <operation access="0" id="" name="Версия ДОП ПО" network="0" />
    </operations>
  </unit>
  <unit id="2" machine="ANYMACHINE" name="ДОП ПО" range="0">
    <operations>
      <operation access="0" id="29" name="BBEE-TDS-Training" network="0">
        <variables>
          <variable coeff="1" offset="0" size="32" type="git"></variable>
        </variables>
      </operation>
      <operation access="0" id="216" name="Sniffer" network="0">
        <variables>
          <variable coeff="1" offset="0" size="32" type="git"></variable>
        </variables>
      </operation>
      <operation access="0" id="220" name="DocumReader" network="0">
        <variables>
          <variable coeff="1" offset="0" size="32" type="git"></variable>
        </variables>
      </operation>
      <operation access="0" id="225" name="FlashMountUtility" network="0">
        <variables>
          <variable coeff="1" offset="0" size="32" type="git"></variable>
        </variables>
      </operation>
    </operations>
  </unit>
</units>
```

## Описание тэгов

- `<units>...</units>` - корневой тэг структуры *xml*-документа
- `<unit>...</unit>` - описание одного устройства. Имеет следующие атрибуты:
	- *id* - номер устройства, соответствующий *deviceId*
	- *name* - имя устройства
	- *range* - начало диапазона *id*, диапазон *id* в *Hex*. В большинстве случаев устанавливается равным `0`
- `<operations>...</operations>` - тэг, обозначающий массив операций для опроса версий
- `<operation>...</operation>` - операция опроса версий. Атрибуты:
	- *access* - уровень доступа от 9 до 0, по убыванию приоритета, при не заполении ставится наивысший - 0. Возможные типы доступа:
		- 0-1: доступны все функции
		- 2-3: нет доступа: сохранение сессии
		- 4:   нет доступа: смена устройства и операции
		- 5:   данные только для чтения
		- 6:   нет доступа: применить
		- 7:   нет доступа: добавление и удаление устройств, открытие и обновление *xml*, сохранение сессии
		- 8:   нет доступа: выход
		- 9:   нет доступа: запрос, интервал запроса, переодический запрос
	- *id* - номер программы из `Programs.set`
	- *name* - имя программы для опроса
	- *network* - тип сети: 0 lan, 1 can low, 2 can hi
- Может записываться как парой тэгов, так и одиночным самозакрывающимся тэгом.
- `<variables>...</variables>` - тэги для внутреннего парсинга переданного значения *QVariant*. Для опроса программ записывается следующим образом:

```xml
<variables>
	<variable coeff="1" offset="0" size="32" type="git">1.9.0</variable>
</variables>
```

## Формирование *.sts* файла

После формирования *xml*-файла для генерации из него *sts* нужно:
1) Открыть *XML* в *StatusManager*
2) Нажать на кнопку '+' в левом верхнем углу для добавления строки
3) В первом столбце строки выбираем устройство (*units* из *xml*)
4) Во втором столбце строки выбираем программу для опроса (*operations* из *xml*)
5) После формирования структуры для опроса нажать кнопку 'Сохранить сессию' для формирования *sts*-файла