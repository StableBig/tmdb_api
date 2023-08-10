# TMDB Film Explorer: Руководство по использованию и документация

## Оглавление

* [Описание проекта](#описание-проекта)
    * [Основные возможности](#основные-возможности)
    * [Как это работает?](#как-это-работает)
    * [Предварительные требования](#предварительные-требования)
    * [Что необходимо для запуска и где это взять?](#что-необходимо-для-запуска-и-где-это-взять)
    * [Как настроить виртуальное окружение?](#как-настроить-виртуальное-окружение)
    * [Как настроить виртуальное окружение?](#как-настроить-виртуальное-окружение)
    * [Установите зависимости](#установите-зависимости)
* [Основные скрипты](#основные-скрипты)
    * [hello_api_TMBD.py](#helloapitmdbpy)
    * [make_own_db.py](#makeowndbpy)
    * [find_similar.py](#findsimilarpy)
    * [search_in_db](#searchindbpy)
* [Вспомогательные скрипты](#вспомогательные-скрипты)
    * [own_db_helpers.py](#owndbhelperspy)
    * [tmdb_helpers.py](#tmdbhelperspy)
* [Лицензия](#лицензия)
* [FAQ](#faq)
* [Ссылки](#ссылки)
* [Цели проекта](#цели-проекта)

## Описание проекта

TMDB Film Explorer - это набор инструментов, разработанный для исследования и анализа данных фильмов из базы данных TMDB (The Movie Database). С его помощью вы можете получать данные о фильмах, создавать свою локальную базу данных с фильмами, а также выполнять поиск и получать рекомендации по похожим фильмам на основе различных критериев.

### Основные возможности

1. Подключение к TMDB API - с помощью предоставляемых инструментов вы можете подключиться к API TMDB и получать оттуда данные.
2. Создание своей локальной базы данных фильмов - с помощью одного из инеструментов можно получить определенное количество данных о фильмах и сохранить их в формате JSON для локального использования.
3. Поиск по своей базе данных - предоставляемые инструменты позволяют выполнять быстрый поиск фильмов по названию в вашей локальной базе.
4. Рекомендации фильмов - основываясь на определенных критериях (таких как принадлежность к коллекции, оригинальный язык, бюджет и жанры), программа анализирует вашу базу данных и предоставляет рекомендации по похожим фильмам.

### Как это работает?

Проект основан на использовании API TMDB. Перед началом работы пользователю необходимо получить свой API ключ. С его помощью мы делаем запросы к базе данных и получаем информацию о фильмах.

Основной акцент делается на создание пользовательской базы данных и дальнейшее взаимодействие с ней, что позволяет работать с данными быстро и без необходимости постоянного подключения к интернету.

### Предварительные требования:

1. Установленный Python версии 3.11.
2. pip - установщик пакетов Python.
3. Virtualenv - инструмент для создания изолированных сред Python.
4. Валидный API ключ для TMDB (для некоторых скриптов).
5. Подключение к Интернету (для некоторых скриптов).

### Что необходимо для запуска и где это взять?

1. Python: https://www.python.org/downloads/.
2. Получите API ключ для TMDB, зарегистрировавшись на [TMDB](https://www.themoviedb.org "The Movie Database(TMDB)").

### Как настроить виртуальное окружение?

Пример создания нового виртуального окружения и его активация:

```bash
python3 -m venv venv
source venv/bin/activate  # для Unix систем
.\venv\Scripts\activate  # для Windows
```

### Установите зависимости

С активированным виртуальным окружением установите зависимости проекта:

```bash
pip install -r requirements.txt
```

### Скрипты проекта:

* [hello_api_TMDB.py](#helloapitmdbpy)
* [make_own_db.py](#makeowndbpy)
* [find_similar.py](#findsimilarpy)
* [search_in_db.py](#searchindbpy)
* [own_db_helpers.py](#owndbhelperspy)
* [tmdb_helpers.py](#tmdbhelperspy)

## Основные скрипты

### hello_api_TMDB.py

#### Что делает скрипт?

С помощью этого инструмента мы настраиваем и проверяем связь с API TMDB (The Movie Database).

Для проверки его работы мы получаем данные с бюджетом определенного фильма.

#### Как запустить скрипт?

```bash
python3 hello_api_TMDB.py
```

#### Что выведет скрипт?

Если все настроено верно и связь с API установлена, мы получим бюджет заданного фильма.

Пример вашего запроса и вывода ответа на запрос:

```
(venv) yourname@yournames-MaxBookPro tmdb_api % python3 hello_api_TMDB.py
Enter your api key v3:
4000000
```

В этом примере мы запускаем файл `hello_api_TMDB.py`, в ответ на запрос ключа API вводим значение нашего ключа (для этого ознакомьтесь с разделом [Что необходимо для запуска и где это взять?](#что-необходимо-для-запуска-и-где-это-взять)).
В ответ на наш запрос получаем число. Это и есть бюджет фильма с указанным номером (по умолчанию номер фильма равен **215**). Если команда выполнена успешно, значит связь с API установлена и работает.

Если API ключ указан неверно, вы получите следующий ответ:

```
Invalid api key
```

И программа завершится. В этом случае пройдите запустите скрипт снова и введите верный API ключ.

### make_own_db.py

#### Что делает скрипт?

Скрипт скачивает данные о заданном количестве фильмов с помощью TMDB API и сохраняет их в файле в формате JSON.

#### Как запустить скрипт?

```bash
python3 make_own_db.py
```

#### Что выведет скрипт?

Скрипт выведет прогресс загрузки данных (в процентах). По завершении создаст файл `MyFilmDB.json` с данными о фильмах.

Пример вашего запроса и вывода ответа на запрос:

```
(venv) yourname@yournames-MaxBookPro tmdb_api % python3 make_own_db.py
Enter your api key v3:
please, wait, this operation may take smth like 15-20 minutes
0.0 percent complete
0.1 percent complete
0.2 percent complete
...
99.8 percent complete
99.9 percent complete
```

В этом примере мы запускаем скрипт `make_own_db.py`, в ответ на запрос ключа API вводим значение нашего ключа (для этого ознакомьтесь с разделом [Что необходимо для запуска и где это взять?](#что-необходимо-для-запуска-и-где-это-взять)).
В ответ на наш запрос получаем прогресс выполнения в процентах: **0.0 percent complete**, **0.1 percent complete**, **0.2 percent complete** и так далее. Обратите внимание, что процесс загрузки занимает какое-то время. По окончании загрузки в корневой директории проекта появится файл `MyFilmDB.json` с содержимым такого вида:

```
[{"adult": false,
  "backdrop_path": "/hQ4pYsIbP22TMXOUdSfC2mjWrO0.jpg",
  "belongs_to_collection": null,
  "budget": 0,
  "genres": [{"id": 18, "name": "драма"},
    ...
    ...
    ...
]
```

### find_similar.py

#### Что делает скрипт?

Скрипт ищет фильмы, похожие на заданный пользователем, на основе определенных критериев, таких как принадлежность к коллекции, оригинальный язык, бюджет и жанры.

#### Как запустить скрипт?

```bash
python3 find_similar.py
```

#### Что дополнительно потребуется?

Потребуется доступ к предварительно созданному файлу с данными `MyFilmDB.json` (файл может называться и по-другому).

Для его создания воспользуйтесь скриптом `make_own_db.py` из настоящего проекта.

Подробное описание скрипта [здесь](#makeowndbpy).

#### Что выведет скрипт?

Скрипт выведет список фильмов, рекомендуемых на основе заданного фильма.

Пример вашего запроса и вывода ответа на запрос:

```
(venv) yourname@yournames-MacBookPro tmdb_api % python3 find_similar.py
Enter path to DataBase:filmDatabase.json
```

В примере выше мы запускаем скрипт `find_similar.py`, в ответ мы получаем предложение ввести путь, ведущий к файлу с данными (JSON файл). Если он находится в той же корневой директории, что и файлы настоящего проекта, то просто указываем название файла с данными. Мы указали `filmDatabase.json` в качестве пути к файлу. Но такого файла в нашем примере не существует. Если путь указан неверно, то получим слудующее сообщение:

```
File not found, sorry...
```

После этого программа завершится.

Необходимо снова пройти все предыдущие шаги и указать верный путь к файлу с данными. Например `MyFilmDB.json`:

```
(venv) yourname@yournames-MacBookPro tmdb_api % python3 find_similar.py
Enter path to DataBase:MyFilmDB.json
```

Путь к файлу с данными указан верно. В ответ мы получим текст с предложением ввести название фильма для поиска:

```
Enter film to search for:Гладиатор
```

Мы указали **"Гладиатор"** в качестве фильма для поиска. Но такой фильм не был найден в файле с данными. Если фильм не найден, мы получим такой ответ:

```
No such film in FilmsDB
```

После этого программа завершится.

Необходимо снова пройти все предыдущие шаги и указать фильм, который есть в файле с данными. Например **"Gladiator"**:

```
(venv) yourname@yournames-MacBookPro tmdb_api % python3 find_similar.py
Enter path to DataBase:MyFilmDB.json
Enter film to search for:Gladiator
```

В ответ мы получим список из похожих фильмов:

```
American Beauty
Citizen Kane
Dancer in the Dark
Finding Nemo
Forrest Gump
Four Rooms
Judgment Night
Life in Loops (A Megacities RMX)
Star Wars
```

И выполнение программы завершится.

_Обратите внимание, что в настоящей базе данных названия фильмов написаны латиницей. API ключ и доступ к интернету не требуется, если вы заранее загрузили базу данных._

#### Особенности скрипта

1. Определение параметров сравнения фильмов.

Чтобы определить какие атрибуты фильма будут учитываться при определении схожести и в какой степени, используется система "веса" атрибутов.

Скрипт "анализирует":

* относится ли фильм к какой-либо коллекции (например, сериалу или франшизе). Вес этого параметра - 1000.
* на каком языке фильм. Вес - 300.
* бюджет фильма. Вес - 100.
* жанры фильма. Вес - 500.

Чем выше значение веса, тем больше значение этого параметра при определении схожести.

2. Вычисление рейтинга схожести.

Рейтинг фильма отражает его схожесть с выбранным фильмом на основе параметров, указанных выше.

* Изначальное значение рейтинга - 0.
* Для каждого параметра, если значение этого параметра для текущего фильма совпадает со значением выбранного фильма, к рейтингу добавляется вес этого параметра.
* Рейтинг для текущего фильма сохраняется в словаре, где ключ - это название фильма, а значение - рейтинг схожести.

3. Удаление выбранного фильма из рейтинга.

Скрипт при подборе рекомендаций удаляет фильм, на основе которого мы хотим получить рекомендации, из списка рейтингов, так как не имеет смысла рекомендовать фильм, который уже был выбран нами.

### search_in_db.py

#### Что делает скрипт?

Скрипт выполняет поиск фильмов на основе заданного пользователем ключевого слова.

#### Как запустить скрипт?

```bash
python3 search_in_db.py
```

#### Что дополнительно потребуется?

Потребуется доступ к предварительно созданному файлу с данными `MyFilmDB.json` (файл может называться и по-другому).

Для его создания воспользуйтесь скриптом `make_own_db.py` из настоящего проекта.

Подробное описание скрипта [здесь](#makeowndbpy).

#### Что выведет скрипт?

Скрипт выведет список всех фильмов в базе данных, которые содержат заданное пользователем ключевое слово в своем названии.

Пример вашего запроса и вывода ответа на запрос:

```
(venv) yourname@yournames-MacBookPro tmdb_api % python3 search_in_db.py
Enter path to DataBase:some_DB.json
```

В примере выше мы запускаем скрипт `search_in_db.py`, в ответ мы получаем предложение ввести путь, ведущий к файлу с данными (JSON файл). Если он находится в той же корневой директории, что и файлы настоящего проекта, то просто указываем название файла с данными. Мы указали `some_DB.json` в качестве пути к файлу. Но такого файла в нашем примере не существует. Если путь указан неверно, то получим слудующее сообщение:

```
File not found, sorry...
```

После этого программа завершится.

Необходимо снова пройти все предыдущие шаги и указать верный путь к файлу с данными. Например `MyFilmDB.json`:

```
(venv) yourname@yournames-MacBookPro tmdb_api % python3 search_in_db.py
Enter path to DataBase:MyFilmDB.json
```

Путь к файлу с данными указан верно. В ответ мы получим текст с предложением ввести название фильма для поиска:

```
Enter film to search for:Гладиатор
```

Мы указали **"Гладиатор"** в качестве ключевого слова для поиска. Но фильмы с таким словом не были найдены в файле с данными. Если фильм, содержащие введенное слово, не найдены, то программа просто завершится.

Необходимо снова пройти все предыдущие шаги и указать слово, которое есть в файле с данными. Например слово **mind**:

```
(venv) yourname@yournames-MacBookPro tmdb_api % python3 search_in_db.py
Enter path to DataBase:MyFilmDB.json
Enter film to search for:mind
```

В ответ мы получим список фильмов, в названии которых есть **mind**:

```
A Beautiful Mind
Eternal Sunshine of the Spotless Mind
```

И выполнение программы завершится.

_Обратите внимание, что в настоящей базе данных названия фильмов написаны латиницей. API ключ и доступ к интернету не требуется, если вы заранее загрузили базу данных._

## Вспомогательные скрипты

Следующие скрипты являются вспомогательными и не запускаются отдельно:

### own_db_helpers.py

Этот скрипт содержит вспомогательные функции для загрузки данных из файла JSON, который создается скриптом **make_own_db.py**.

### tmdb_helpers.py

Этот скрипт содержит вспомогательные функции для выполнения запросов к API TMDB и загрузки ответа в формате JSON.

## Для разработчиков

В скрипте `hello_api_TMDB.py` по умолчанию номер фильма равен **215**. Для изменения номера фильма поменяйте число в переменной `movie_number`._

## Лицензия

Текст лицензии доступен в файле [LICENSE](./LICENSE).

## FAQ

#### Что такое TMDB (The Movie Database)?

Это популярная редактируемая пользователями база данных фильмов и сериалов.

## Ссылки

[TMDB (The Movie Database)](https://themoviedb.org/).

[Документация TMDB для разработчиков](https://developer.themoviedb.org/docs).

## Цели проекта

Проект написан в образовательных целях.
