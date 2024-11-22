# Опросник
Данный небольшой проект создан для опроса ИОГВ (Исполнительный Орган Государственной Власти) Санкт-Петербурга.
Проект расположенный в этом репозитории является форком оригинального [проекта](https://github.com/dobrodelete/Survey) с добавлением nginx и исправлением docker-compose.yml
в котором не был подключен том reports-data:/app/reports/json из-за чего возникала ошибка открытия файла опроса и ошибкой 500 internal server error
## Установка с помощью docker compose
### Установка docker engine
#### Ubuntu:
https://docs.docker.com/engine/install/ubuntu/
#### Post-installation steps for Docker Engine:
https://docs.docker.com/engine/install/linux-postinstall/

#### Установка git:
```
sudo apt install git
```
### Скачивание проекта на сервер и его установка:
```
git clone https://github.com/drumlast/Survey-fork.git
```
```
cd Survey-fork
```
```
docker compose up --build -d
```
Проверяем, что все контейнеры запустились и работают командой:
```
docker ps
```
Затем перейти в браузере по адресу: http://IP-ADDRESS-OR-YOUR-DOMAIN/

Если необходимо включить https - необходимо подготовить SSL-сертификат и приватный ключ, скинуть их в папку certs/ , в конфигурационном файле nginx.conf, расположенном в папке со скачанным проектом - необходимо снять комментарии и подключить сертификат и ключ в этом конфигурационном файле. После этого выполнить:
```
docker compose down
```
Дождаться остановки контейнеров и потом:
```
docker compose up -d
```

## Установка и настройка вручную.
### Установка Python
#### Windows
Скачиваем Python с официального [сайта](https://www.python.org/downloads/).
После скачивания .exe мы запускаем файл и проходим самую обычную установку. Важно установить пункт "Добавить в PATH".
### Установка проекта.
Скачиваем проект. Это можно сделать прямо из github zip архивом:
![фото](docs/images/git-download-zip.png)

После скачивания мы переходим в папку, заранее её разархивировав.

### Запуск проекта.
При установке python должен был быть установлен установщик модулей и библиотек pip.
Нам надо открыть PowerShell или CommandPrompt (командная строка) от имени администратора, перейти в папку.

Вводим следующую команду, для того, чтобы можно было работать с виртульным окружением для проекта:

`Set-ExecutionPolicy Unrestricted`(PowerShell)

Если у вас не работает pip, то его нужно установить:

`curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py`(Command Prompt)
`python get-pip.py`(Command Prompt)

#### Устанавливаем виртуальное окружение.
Устанавливаем виртуальное окружение:

`python -m pip install --user virtualenv`

Создаём виртуальное окружение:

`python -m venv venv`

После установки, в текущей директории должна была появиться папка `venv`
Если она есть, то значит что виртуальное окружение успешно было установлено. Далее нам надо запустить виртуальное окружение:

`.\venv\Scripts\activate`(Command Prompt)
`.\venv\Scripts\Activate.ps1`(PowerShell)

#### Установка модулей и библиотек.
Для установки нужных зависимостей мы запускаем следующую команду:

`pip install -r requirements.txt`

#### Настройка проекта и создание бд.
В файле `config.py` мы можем изменить настройки, в том числе логин и пароль администратора.
Админ панель пока что находится в разработке, поэтому логин и пароль носят относительных характер, но всё-таки логин и пароль важно поменять.

Для небольшой настройки и для корректной работы сайта, надо запустить следующий скрипт:

`python setup.py`

#### Запуск проекта:
Для отладки проекта и в случае возникновения багов и ошибок, в настройках (`config.py`) стоит режим отладки:
`FLASK_DEBUG = True`

Если вы не хотите, чтобы появлялись ошибки, то следует заменить `True` на `False`.

Для запуска проекта достаточно прописать:

`python main.py`

Для открытия сайта, можно перейти по адресу: `http://127.0.0.1:5000` и у вас откроется сайт, который можно посмотреть, потестировать и если что написать автору проекта свои замечания и прочее.

## Установка из архива.
Это подойдёт тем, кто не хочет делать всё руками.
Для получения актуального архива, напишите в телеграм: @dobrodelete

В этом случае надо будет только скачать python, убедиться что у вас есть pip, установить pip если потребуется, запустить виртуальное окружение и запустить сам проект.