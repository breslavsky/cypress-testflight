# Туториал: исследуем баги и пишем профессиональные баг-репорты

Подойдет тем, что хочет научиться исследовать ошибки в ПО и писать профессиональные баг-репорты.

# 👍 Что сделаем

* Проведем исследование **критического бага**.
* Поработаем с **инструментами разработчика** Chrome.
* Больше узнаем про **фронтенд**,  **бекенд**,  **куки**,  **API**,  **лог-файлы** и **SQL**.
* Выполним **SQL-запросы** в базу данных.
* Напишем **профессиональный баг-репорт**.

# 🙋‍️ Перед началом

* У Вас установлен браузер [Google Chrome](https://www.google.com/chrome/)
* У Вас открывается [тестовое приложение](https://ibank.epic1h.com)
* У Вас установлено приложение для создания скриншотов и записи экрана или установите [Awesome Screenshot](https://www.awesomescreenshot.com)
* Почитайте про [Markdown](https://ru.markdown.net.br/nachinaya/)
* Почитайте про [SQL](https://habr.com/ru/post/480838/)
* Попробуйте поработать с [Markdown таблицами](https://www.tablesgenerator.com/markdown_tables)

Создайте текстовый файл `env.txt` на рабочем столе, заполните и сохраните его со своими данными:
* **Устройство:** MacBook M1 Pro (14-inch, 2021) / 32 GB RAM
* **ОС:** macOS Monterey 12.0.1
* **Экран:** Built-in XDR Display 3024x1964
* **Браузер:** Google Chrome 100.0.4896.88 (arm64)
* **Параметры сети:** 90.187.49.33, 100MB, Vodafone Germany

> env - сокращение от environment - окружение

<details>
   <summary>Откуда это взять ❓</summary>

* **Устройство** — посмотрите этикетки на вашем системном блоке или ноутбуке
* **ОС** — посмотрите [видео](https://www.youtube.com/watch?v=VyvSqajg9C4)
* **Экран** — посмотрите короткое [видео](https://www.youtube.com/watch?v=ak53URhvGzI)
* **Браузер** — посмотрите короткое [видео](https://www.youtube.com/watch?v=2l5Ij77DvQk)
* **Параметры сети** — зайдите на сайт https://whatismyipaddress.com/
</details>

# 😍 Живая обратная связь

Каждый вторник и четверг я провожу бесплатные онлайн стендапы в Zoom.

Если у тебя есть вопрос или проблема, подключайся:
- [x] В **18.00** по Москве нажми на [ссылку](https://us05web.zoom.us/j/6630696938?pwd=UktVaVkxL0puajd5T3ZicHZPY2FuUT09)
- [x] Подними руку или напиши вопрос в чате.
- [x] В случае необходимости, будь готов пошарить свой экран.

@[Anton Breslavsky|https://t.me/breslavsky_anton|https://s.epic1h.com/api/public/dl/nfCyhZhd?inline=true]

Что бы следить за анонсами новых туториалов подписывайся на [телеграмм канал](https://t.me/epic_one_hour)

***

# 🔢 Шаги

## 1. Оформляем баг-репорт

- [x] Открой в **Chrome** https://ibank.epic1h.com/?v=1.1
- [x] Попробуй войти в личный кабинет пользователем **marry** с паролем **qwerty**

<details>
  <summary>Что такое qwerty 🤢?</summary>

<img class="cornered" src="img/qwerty.gif" width="465" height="600">

</details>

❗ После нажатия на кнопку **Войти** пользователю выдается сообщение **Критическая ошибка сервера**.

- [x] В новой вкладке снова открой **Markdown** редактор https://markdownlivepreview.com/
- [x] Скопируйте в него исходное содержимое [шаблона идеального баг-репорта](/artefacts/perfect_bug_report.md?plain=1)

**Поправьте в репорте:**
* Дату обнаружения.
* Версию приложения.
* Окружение.

***

## 2. Воспроизводим и исследуем баг

- [x] Сделай запись экрана используя **Awesome Screenshot** и закрепите ссылку в отчет.
- [x] Очисти результаты исследования в репорте и оставьте только заголовки.

***

### Состояние до бага

Выполните предварительные условия:
- [x] Открой https://ibank.epic1h.com/?v=1.1
- [x] Сбрось **Cookie** и кэш в Браузере: **Инструменты разработчика** &rarr; **Приложение** &rarr; **Хранилище** &rarr; **Очистить**

***

Выполни шаги для воспроизведения бага:
- [x] Открой главную страницу `/` iBank.
- [x] В разделе **Исследование** заполни подразделы **После загрузки страницы**.

#### Консоль

- [x] В **Инструментах разработчика** перейдите на вкладку **Консоль**.
- [x] Скопируй содержимое консоли в раздел баг-репорта **6.1. Console пользователя**.

> Не забывайте оформлять **Markdown**
> ~~~Markdown
> ```text
> Текст тут
> ```
> ~~~

<details>
  <summary>Что получилось</summary>

~~~Markdown
```text
фронтенд загружен
запрос на бекенд GET /api/users/summary
ответ сервера: {count: 3}
Uncaught TypeError: final is not a function at XMLHttpRequest.request.onreadystatechange
```
~~~
</details>

#### Cookies

- [x] Перейди на вкладку **Приложение** &rarr; **Cookies** и заполните в отчете **6.2. Cookie браузера**.

Используйте [Markdown таблицы](https://www.tablesgenerator.com/markdown_tables) для оформления.

<details>
  <summary>Что получилось</summary>

~~~Markdown
```markdown
| **name** | **value**           |
|----------|---------------------|
| rnd      | 0.22187308399860428 |
```
~~~
</details>

***

#### Запросы к API

- [x] Перейди на вкладку **Сеть** и выберите фильтр **Fetch/XHR**.
- [x] Выбери запрос `/summary`, заполните **6.3. Log запросов к API** &rarr; **После загрузки страницы**.
- [x] Используй вкладки **Заголовки**, **Ответ**, **Cookies** и шаблон:

~~~Markdown
```text
{Request Method} {Request URL}
{Status Code} ↓ 
{Response}
```
~~~

<details>
  <summary>Что получилось</summary>

~~~Markdown
```text
GET https://qa.ecpic1h.com/api/users/summary
200 ↓ 
{"count": 5}
```
~~~
</details>

***

#### Состояние базы данных

- [x] Перейди на https://ibank.epic1h.com/db.html и выполните запрос:

```sql
SELECT id, username, password, firstName FROM users WHERE username = 'marry'
```

- [x] Используй [Markdown таблицы](https://www.tablesgenerator.com/markdown_tables) для оформления.

<details>
  <summary>Что получилось</summary>

~~~Markdown
Пользователь с логином `marry` присутствует в базе данных.

```markdown
| **id** | **username** | **password** | **firstName** |
|--------|--------------|--------------|---------------|
| 3      | marry        | qwerty       | NULL          |
```
~~~
</details>

- [x] Проверь что сессии для пользователя **marry** отсутствуют:

```sql
SELECT * FROM sessions WHERE user = 2
```

***

### Исследуем состояние после обнаружения бага

- [x] Выполни оставшиеся шаги для воспроизведения

2. На форме **Входа** заполнить поля:
    1. Логин: **marry**
    2. Пароль: **qwerty**
3. Нажать на кнопку **Войти**

#### Консоль

- [x] Скопируй новые записи в раздел **После нажатия на кнопку Войти**

<details>
  <summary>Что получилось</summary>

~~~Markdown
```text
запрос на бекенд POST /api/login {username: 'marry', password: 'qwerty'}
POST https://ibank.epic1h.com/api/login 500 (Internal Server Error)
```
~~~
</details>

***

#### Cookies

- [x] Заполни состояние Cookies.

<details>
  <summary>Что получилось</summary>

Без изменений.
</details>

***

#### Запросы к API

- [x] Опиши все запросы к API после фиксации бага.

<details>
  <summary>Что получилось</summary>

~~~Markdown
### После нажатия на кнопку **Войти**
```
POST /api/login
{"login": "marry", "password": "qwerty"}
500 ↓
Не удалось создать сессию
```
~~~
</details>

***

#### Состояние базы данных

- [x] Проверь сессии для пользователя **marry** и добавьте в отчет.
```sql
SELECT * FROM sessions WHERE user = 2
```

<details>
  <summary>Что получилось</summary>

~~~Markdown
Создана сессия для пользователя `marry`

`SELECT * FROM sessions WHERE user = 2`

| **id**    | **user** | **active** |
|-----------|----------|------------|
| eeSJFLKxt | 3        | 1          |
~~~
</details>

***

#### Лог сервера

- [x] Открой в новой вкладке о https://ibank.epic1h.com/server.log
- [x] Добавь в отчет информацию которую считаете ключевой.

<details>
  <summary>Что получилось</summary>

~~~Markdown
```text
2022-05-01T12:18:46.792Z connected to database
2022-05-01T12:18:46.791Z server has been started
...
2022-05-01T12:18:49.049Z checking password qwerty === qwerty
2022-05-01T12:18:49.049Z finding username marry
2022-05-01T12:18:49.050Z TypeError: Cannot read property 'toUpperCase' of null
```
~~~
</details>

# Фидбек пожалуйста 🙏

? Полезный материал ?
* 🤩 Очень полезный материал
* 😃 В целом полезный
* 😐 Возможно что-то пригодится
* 😒 Нет ничего полезного
* 😬 Абсолютно бесполезно

? Все ли было понятно ?
* 🤩 Все понятно на 100%
* 😃 В целом все понятно
* 😐 Что-то понятно, что-то нет
* 😒 Понял только малую часть
* 😬 Ничего не понял

? Как тебе такой формат туториала ?
* 🤩 Очень удобно
* 😃 Мне понравилось
* 😐 Нормально
* 😒 Не удобно
* 😬 Ужасно

# Артефакты
1. [Баг и баг репорт](https://beqa.pro/blog/баг-и-баг-репорт)
2. [Правила написания предварительных шагов в тест-кейсах](https://habr.com/ru/post/481628/)
