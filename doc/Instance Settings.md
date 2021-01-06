# Настройки экземпляра

## Запуск браузера в режиме headless

Используйте параметр `headless_browser` для запуска бота через интерфейс командной строки. Этот способ отлично работает при запуске сценариев локально или для развертывания на сервере. Нет графического интерфейса GUI и соответственно меньше нагрузка на процессор.

![BhEgXANLhJ](C:\Users\Андрей\Desktop\BhEgXANLhJ.gif)



> Предупреждение: некоторые пользователи не рекомендуют использовать эту функцию, поскольку *Instagram* может [распознать работу браузера в *headless* режиме ](https://antoinevastel.com/bot%20detection/2017/08/05/detect-chrome-headless.html)!

```python
session = InstaPy(username='test', password='test', headless_browser=True) 
```

(Альтернативный вариант) Если используемый вами веб-драйвер не поддерживает *headless* режим (или работа в *headless* режиме становится очень заметна), вы можете использовать параметр `nogui`, который отображает окно вне поля зрения экрана. Имейте в виду, что этому параметру тем не менее не хватает поддержки и простоты использования, он поддерживается только операционными системами на базе Linux (или теми, у которых есть программное обеспечение для отображения *Xvfb*, *Xephyr* и *Xvnc*).

```python
session = InstaPy(username='test', password='test', nogui=True)
```

## Обход системы обнаружения подозрительных попыток входа

*InstaPy* автоматически определяет, активен ли запрос кода безопасности *Security Code Challenge*, и если да, то попросит ввести его через терминал.

Код безопасности из *Instagram* отправляется на вашу электронную почту или по SMS , электронная почта является вариантом выбранным по умолчанию, но вы также можете выбрать вариант с SMS, используя следующие значения параметров: `bypass_security_challenge_using='sms'` или `bypass_security_challenge_using='email'`. 

```python
InstaPy(username=insta_username, password=insta_password, bypass_security_challenge_using='sms')
```

## Двухфакторная аутентификация 

*InstaPy* автоматически определяет, защищена ли учетная запись с помощью двухфакторной аутентификации. Если да, то пользователю *InstaPy* необходимо передать в конструктор, текущего сеанса работы коды безопасности. Для корректной работы требуется ввести хотя бы один код.

Коды безопасности можно найти в `Instagram` по следующему пути: **Settings** -> **Security** ->**Two-Factor-Authentication**->**Backup Codes**.

```python
InstaPy(username=insta_username, password=insta_password, security_codes=(["01234567","76543210","01237654"])
```

## Используем прокси

Вы можете использовать *InstaPy* через прокси, указав адрес сервера, порт и/или учетные данные для аутентификации на прокси сервере. Этот способ работает как с опцией `headless_browser`, так и без нее.

Пример простой настройки прокси:

```python
session = InstaPy(username=insta_username, password=insta_password, proxy_address='8.8.8.8', proxy_port=8080)
```

Настройка прокси с примером аутентификации:

```python
session = InstaPy(username=insta_username, password=insta_password, proxy_username='', proxy_password='', proxy_address='8.8.8.8', proxy_port=4444)
```

## Проверяем состояние интернет-соединения

*InstaPy* может выполнить несколько типов проверок соединения, включая состояние вашего соединения, а также доступность серверов *Instagram*. Эти проверки иногда не проходят, потому что *Instapy* использует сторонние сервисы для их выполнения. Для этого вы можете переопределить настройки проверок с помощью опции `want_check_browser`.

Значение `want_check_browser` по умолчанию принято `False`, но вы можете установить его в `True` при запуске текущего сеанса работы. Рекомендуем сделать это, если вы хотите осуществлять дополнительные проверки подключения к сети и серверам `Instagram`.

Например:

```python
session = InstaPy(username=insta_username, password=insta_password, want_check_browser=True)
```

## Запуск сеансов в отдельных потоках

Если вы запускаете *InstaPy* в потоках и получаете исключение вида `ValueError: signal only works in main thread`, вам необходимо корректно завершить сеанс работы. Вы можете сделать это двумя способами.

Завершить сеанс в контексте `smart_run`:

```python
session = InstaPy()
with smart_run(session, threaded=True):
    """ Активный поток """
    # некоторые действия ...
```

Завершить сеанс вызвав метод `end`:

```python
session = InstaPy()
session.login()
# некоторые действия ...
session.end(threaded_session=True)
```

## Выбираем версию браузера

Если, например, в вашей системе установлено несколько версий *Firefox* или если вы используете его *portable* версию, вы можете указать *InstaPy* использовать определенную версию браузера с помощью опции `browser_executable_path` при инициализации экземпляра класса.

> Указав путь к исполняемому файлу *Firefox*, вы можете получить следующее сообщение об ошибке: `selenium.common.exceptions.SessionNotCreatedException: Message: Unable to find a matching set of capabilities`.  Это свидетельствует о том, что текущая версия браузера не обеспечивает наличия необходимого набора возможностей браузера для дальнейшей работы. Обычно это случается если вы используете старую версию браузера и для дальнейшей работы рекомендуется использовать версию новее.

Пример с операционной системой Windows (с соответствующими путями также будет работать в Linux и macOS).

```python
session = InstaPy(username=insta_username, password=insta_password, browser_executable_path=r"D:\Program Files\Mozilla Firefox\firefox.exe")
```

