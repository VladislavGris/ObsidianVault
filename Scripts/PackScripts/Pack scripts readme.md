---
tags:
  - work
  - docs
---
[[Pack file versions to stars]]
[[Dependencies from lock file]]
[[Stars to versions]]
## Содержание скриптов

- `upversion.sh` - общий управляющий скрипт, вызывает все остальные    скрипты. 
* *1-й аргумент командной строки*: имя артефакта. 
- Пример использования:
```bash
./scripts/upversion.sh client
```

- `versionToStar.py` - скрипт преобразует все версии в переданном `.yml`-файле в символ '\*'.
- *1-й аргумент командной строки*: путь к `.yml`-файлу.
- Пример использования:
```bash
python3 versionToStar.py client.yml
```

- `getDepsFromLock.py` - скрипт формирует список зависимостей и их версий из `.lock`-файла. *1-й аргумент командной строки*: путь к `.lock`-файлу.
- Пример использования:
```bash
# Стандартный поток вывода перенаправляется в .txt файл
python3 scripts/getDepsFromLock.py client.lock > client.txt
```

- `updateVersions.py` - скрипт преобразует символы '\*' в версиях на последние мажорные версии зависимостей в виде `[~=3]`. 
- *1-й аргумент командной строки*: путь к файлу со списком зависимостей и версий.
- *2-й аргумент командной строк*: путь к `.yml`-файлу для обновления версий.
- Пример использования:
```bash
python3 scripts/updateVersions.py client_deps.txt client.yml
```