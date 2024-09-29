# **STT для игры SS14 для сервера Orienta**

## Релизная версия

<!-- markdownlint-disable -->

## Описание проект

Данный проект представляет релизную версию TTS сервера на Python для игры SS14. !В данном гите нет информации как подключить клиент игры SS14 к данному серверу!

В случае если вам необходимо реализация клиента SS14 для подключения к данному серверу, необходимо обращаться к разработчикам и владельцам(-у) сервера Orienta

## Использованные библиотеки, пакеты и модель для распознования

В качестве STT распознования была выбрана библиотека и модель от OpenAI - [Fast Whisper] (https://github.com/SYSTRAN/faster-whisper).

Библиотеки для Python сервера:
```bash
pip install websockets
pip install faster-whisper
pip install soundfile
pip install numpy
```
<b>Так же необходимо установить поддержку CUDA ядер. torch нужной версии уже находится в fast-whisper </b>
<b> Проект не будет работать без CUDA!!!</b>
Советую так же ознаокмится с гайдами по установке torch, так как там нужно так же устанавливать специальные драйверы для Nvidia 

Библиотеки для тестового клиента на C# (Если вы работаете в Visual Studio, то данные команды достаточно вести в "Консоль диспетчера пакетов"):
```bash
Install-Package NAudio
```

Необходимые пакеты для сокета должны быть установлены по умолчанию в пакете NET.
 

## Начало работы

После установки пакетов, вам необходимо запустить main.py (сервер).
При первом запуске или перезагрузке сервера будет длительная загрузка модели (в данном случае large).
На гите Fast Whisper вы можете найти все модели, убедитесь что они поддерживают русский язык.

После получения сообщения "Сервер начал свою работу", ваш сервер готов получать данные от клиента.
<b> Для проверки вы можете запустить тестовый клиент на C#, чтобы убедится что всё работает корректно </b>
Для этого после запуска клиента необходимо дождаться подключения, ввести "r", сказать в микрофон фразу, и нажать Enter.
Сервер в логах сообщит о получении сообщения и сообщит распознаный текст, который отобразится в клиенте.
<b> Для проверки нескольких клиентов в Visual Studio можно запустить несколько клиентов (кнопка правее от обычного запуска проекта, иконка запуска не закрашенная)</b>

## Технологии

В сервере предусмотрена асинхронность и асинхронная очередь. Это означает что данный сервер будет не последовательно обрабатывать каждый запрос, а работать с каждым запросом одновременно.
<b> Это существено ускоряет его работу </b>

Так же используются CUDA ядра, при помощи чего Fast Whisper способна осуществлять распознование и вывод результата чуть ли не в реальном времени.
<b> Стоит отметить что WER у large модели Fast Whisper для русского языка составляет около 10%, что есть хорошая точность при удивительной скорости </b>


## Унструкция по подключения клиента игры SS14 к серверу

На вход сервер должен получать <b> бинарные данные аудио </b> (аудио в wav формате). Данный способ не требует особых библиотек.

После обработки сервер получает распознанный текст, и отправляет <b> распознанный текст в исходном виде </b> (без преобразований) клиентской части. Это так же стандартный метод для сокетов

При такой передаче не должно возникать проблем. Убедитесь что ваш клиент будет отправлять <b> бинарные данные аудио </b>, а <b> НЕ само аудио в исходном виде </b>


## Лицензии

Мой код сервера является общедоступным и свободным к копированию. <b> Клиентская часть </b> игры SS14 в данном проекте не представляется. 
В случае вопросов и сотрудничества стоит обращаться к разработчикам и владельцам(-у) сервера Orienta.

<b> При возникновении проблем с подключением к серверу или иными проблемами с сервером можно обращаться ко мне или писать в Issue во вкладке данного проекта на GitHube </b>
