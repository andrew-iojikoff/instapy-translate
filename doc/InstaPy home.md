# InstaPy

Инструмент, который **автоматизирует** ваши действия в социальных сетях для «фарма» лайков, комментариев и подписчиков в Instagram, реализованный на Python с использованием модуля Selenium.

## Установка 

```shell
pip install instapy
```

**Важно**: в зависимости от вашей системы используйте `pip3` и `python3`.

Если вы используете *Ubuntu*, прочтите специальное руководство по [установке в Ubuntu (64-бит)](https://github.com/InstaPy/instapy-docs/blob/master/How_Tos/How_To_DO_Ubuntu_on_Digital_Ocean.md) . Если вы используете Raspberry Pi, ознакомьтесь с руководством по [установке на RaspberryPi](https://github.com/InstaPy/instapy-docs/blob/master/How_Tos/How_to_Raspberry.md).

Если вы хотите установить определенную версию *Instapy*, то вы можете сделать это с помощью:

```shell
pip install instapy == 0.1.1
```



### !!! Запуск Instapy 

Чтобы запустить InstaPy, вам нужно запустить скрипт **[быстрого](https://github.com/InstaPy/instapy-quickstart)** запуска, загруженный по ссылке.

- [Вот самый простой сценарий **быстрого запуска,** который вы можете использовать](https://github.com/InstaPy/instapy-quickstart/blob/master/quickstart.py)
- [Здесь вы можете найти множество сложных шаблонов для **быстрого старта,** которыми поделились сообщество!](https://github.com/InstaPy/instapy-quickstart/tree/master/quickstart_templates)

Теперь вы можете ввести данные своей учетной записи, передав параметры имя пользователя `username` и пароль `password` в функцию `InstaPy()`, которая находится в вашем сценарии **быстрого запуска** , например так:

```python
InstaPy(username="abcd", password="1234")
```

Или же вы можете [передать их с использованием интерфейса командной строки (CLI)](https://instapy.org/additional-information#pass-arguments-by-cli).

После того, как вы настроили сценарий **быстрого запуска,** вы можете выполнить его с помощью следующих команд.

```shell
python quickstart.py
# или
python quickstart.py --username abcd --password 1234
```

InstaPy откроет окно браузера и начнет работу.

> Если вы хотите, чтобы InstaPy работал в фоновом режиме, при запуске из интерфейса командной строки передайте опцию `--headless-browser`  или добавьте параметр`headless_browser=True` в конструктор `InstaPy(headless_browser=True)`.

## Обновление InstaPy

```shell
pip install instapy -U
```

