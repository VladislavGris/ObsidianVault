---
tags:
  - docs
  - work
info:
  - apps
  - bbee
---
### Общая структура настроек

Стандартная папка с настройками: `/mnt/hda2/Configurations`. Ее содержимое копируется на все 4 абока при деплое.
Внутренняя сеть: `192.168.1.*`, где `*` - номер устройства.
Устройства, их конфиги и конфиги, которые нужно сохранять:
1) АРМК: `../BBEE-AWC`
	- BBEE-AWC-DTM.set
2) СОЦ: `../BBEE-TDS`
	- BBEE-AwsTds.set
	- BBEE-MarkDetector.set
3) ССЦ: `../BBEE-TTS`
4) ТОВ: `../BBEE-TOS`
	- BbeeTos.set

### Механизм работы

- Существуют 4 абокса, 1 - арм-к (управляющий в данном случае)
- Для сохранения есть 2 расположения:
	1) **Конфигурационный носитель**: `/mnt/hda2/DefaultConfigurations`
	2) **Системный носитель**: `/start/DefaultConfgirations`
- При сохранении настроек устройств необходимые конфиги сохраняются на АРМ-К по одному из выбранных путей (системный или конфигурационный носитель). Например:

>[!example] Сохранение настроек **СОЦ**
> 1) Для сохранения используется системный носитель
> 2) Копируем данные файла `BBEE-AwsTds.set` и сохраняем в `DefaultBBEE-AwsTds.set`
> 3) Копируем данные файла `BBEE-MarkDetector.set` и сохраняем в `DefaultBBEE-MarkDetector.set`
> 4) Содержимое директории `/start/DefaultConfgirations` после сохранения настроек **СОЦ**:
> ./start/DefaultConfigurations
├── DefaultBBEE-AwsTds.set
└── DefaultBBEE-MarkDetector.set

- При установке конфигов на устройства сохраненные настройки по умолчанию копируются не только на устройство, с которого были сохранены, а на все устройства. Например:

> [!example] Сохранение настроек на устройства
> 1) Имеем структуру файлов с настройками по умолчанию из прошлого примера
> 2) Для установки настроек на устройства также необходимо выбрать носитель, с которого они будут устанавливаться. В данном случае системный носитель, т.к. на него осуществляли сохранение
> 3) При нажатии кнопки установки настроек на устройства файлы `DefaultBBEE-AwsTds.set` и `DefaultBBEE-MarkDetector.set` будут сохранены в файлы `BBEE-AwsTds.set` и `BBEE-MarkDetector.set` соответственно и расположены в директории `/mnt/hda2/Configurations/BBEE-TDS` на каждом из 4 абоксов, вне зависимости от того, откуда они были считаны
> 4) В результате файлы `BBEE-AwsTds.set` и `BBEE-MarkDetector.set` на всех 4 абоксах будут **одинаковые**

- Диаграмма сохранения/установки настроек:
![[Backup-restore diagramm]]

- При установке настроек на устройства мы всегда копируем на все 4 устройства; если какое-то из устройств не выбрано, то на все устройства не копируются его настройки
- Для записи в `/start/DefaultConfigurations` нужно выполнить команду:

```bash
sudo mount -o remount,rw / # /start не имеет отдельного раздела, поэтому маунтим /
```

- После окончания работы программы вызываем команду:

```bash
sudo mount -o remount,ro /
```

- Вызывается для возврата системы в `read-only` состояние, исполняется в *detached* режиме, чтобы процесс завершился и после остановки работы программы
### Итог

- Сохранение настроек происходит с указанных устройств одиночными файлами на **АРМК** в директорию по выбору (конфиг или системная)
- Устанавливаются настройки с **АРМК** на все устройства, но располагаются они в необходимые директории: настройки ТОС - в папку ТОС, СОЦ - в СОЦ и т.д.
- После установки указанные файлы на всех абоксах должны быть одинаковые