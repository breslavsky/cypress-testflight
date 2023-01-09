# Туториал: заканчиваем мама проект

Подойдет тем, кто хочет покрыть тестами целый проект на Cypress и добавить его к себе в **портфолио.**

# 👍 Что сделаем

* Напишем еще 10+ тестов для приложения блогов.
* Научимся делать декомпозицию UI.
* Закрепим скилл написания тест-кейсов в Markdown.
* Организуем код на проекте по феншую.
* В качестве бонуса: напишем скрипт загрузки файлов на JS.

# 🙋‍ Перед началом

* Ты инициализировал чистый **Node.js** проект `%/projects/cypress/finish_mama_project`
* Ты установил Cypress `npm i cypress@9 --save-dev`

# 💪 Минутка мотивации

Твои коллеги по команде написали приложение для ведения блогов — аналог https://vc.ru/

Ты должен помочь 💪 им выпустить качественный продукт на рынок.

* Это действительно важный туториал в твоей карьере.
* Если ты самостоятельно сможешь написать все тесты — считай ты **уверенный Junior.**
* Потом зальешь проект на GitHub, и будет чем похвастаться 😜

<iframe src="https://giphy.com/embed/24xRxrDCLxhT2" width="480" height="270" frameBorder="0" class="giphy-embed" allowFullScreen></iframe>

# 🫵 Наставления

**Помни:** никто тебя ничему не научит, если ты сам этого не захочешь!

* Не пропускай шаги.
* Конспектируй.
* Экспериментируй с кодом.
* Разбирай и исследуй эталонный код мастера.
* Записывай вопросы с примерами кода для стендапов с мастером.
* **Не должно остаться ни одной строки кода, которую ты не понимаешь!**

***

# 🔢 Шаги

## +1. Заливаем наработки

Возвращаемся к мама проекту [Conduit](https://demo.realworld.io/)

Как ты помнишь в `README` на [GitHub](https://github.com/gothinkster/realworld) мы
нашли [спецификацию на роутинг](https://realworld-docs.netlify.app/docs/specs/frontend-specs/routing/) — что дает нам представление о функциональных возможностях приложения.

* ❓ Что такое **спецификация**?
* ❓ Что такое **роутинг**?

### +1.1. Создаем README для тест-кейсов

- [x] Создай файл `~/test_cases/README.md`
- [x] Добавь Markdown:

```markdown
This file contains test cases for [Conduit](https://demo.realworld.io/) project.

# Sign up

* [x] [register user](register_user.md)
* [x] [login user](login_user.md)
* [x] [logout user](logout_user.md)

# Articles

## CRUD

* [x] [publish article](articles/crud/publish_article.md)
* [x] [delete article](articles/crud/delete_article.md)
* [x] [edit article](articles/crud/edit_article.md)

* [ ] global articles feed
```

- [x] Открой файл в режиме просмотра.

* ❓ Что такое `CRUD`?
* ❓ Почему ссылки с `[x]` не открываются?

***

### +1.2. Загружаем тест-кейсы

Мы **уже разработали** часть тестов в прошлых туториалах. Как **доставить** этот код в текущий проект?

Все файлы лежат на [GitHub](https://github.com/breslavsky/hello-cypress/tree/main/test_cases/) и можно скачать их
ручками, но ты же девелопер 🧑‍💻

**Задача:** загрузить
файлы [register_user.md](https://raw.githubusercontent.com/breslavsky/hello-cypress/main/test_cases/register_user.md)
и [login_user.md](https://raw.githubusercontent.com/breslavsky/hello-cypress/main/test_cases/login_user.md)
автоматически.

- [x] Установи wget `npm i node-wget --save-dev`
- [x] Установи **базовый URL** в терминале, что бы не повторять его в командах:

```bash
BASE_URL=https://raw.githubusercontent.com/breslavsky/hello-cypress/main
```

- [x] Проверь, что **переменная окружения** установлена:

```bash
echo $BASE_URL
```

* ❓ Что такое переменная окружения?
* ❓ Что делает `echo`?

***

- [x] Проверь, что **полный URL** до файла формируется:

```bash
echo $BASE_URL/test_cases/register_user.md
```

- [x] Загрузи файл `register_user.md`

```bash
npx wget -d test_cases/ $BASE_URL/test_cases/register_user.md
```

- [x] Загрузи файл `login_user.md`

```bash
npx wget -d test_cases/ $BASE_URL/test_cases/login_user.md
```

- [x] Проверь, что файлы в папке `~/test_cases` появились.

* ❓ Что такое полный URL?
* ❓ Что сделал `wget`?
* ❓ Зачем нужен параметр `-d`?

Осталось еще 10+ файлов и можно повторить команду еще много раз 😱

<iframe src="https://giphy.com/embed/8vUEXZA2me7vnuUvrs" 
  width="480" height="480" frameBorder="0" class="giphy-embed"></iframe>

***

### +1.3. Пишем скрипт загрузки файлов

<details>
    <summary>Если ты на Windows 🙋‍</summary>

- [x] Поменяй символ переноса строки с `\r\n` на `\n` в настройках Visual Code

<img class="cornered" width="500px" height="380px" src="assets/vs_eol.png">

* ❓ Что такое `EOL`?
* ❓ Что такое `CRLF`?
* ❓ Что такое `LF`?

- [x] В качестве терминала открой **Git Bash**

<img class="cornered" width="200px" height="256px" src="assets/vs_bash.png">

* ❓ Что такое `Git`?
* ❓ Что такое `Bash`?

</details>

- [x] Создай файл `mama_files.txt`

```text
test_cases/register_user.md|test_cases/
test_cases/login_user.md|test_cases/
test_cases/logout_user.md|test_cases/
test_cases/articles/crud/publish_article.md|test_cases/articles/crud/
test_cases/articles/crud/delete_article.md|test_cases/articles/crud/
test_cases/articles/crud/edit_article.md|test_cases/articles/crud/

cypress/fixtures/me-user.json|cypress/fixtures/

cypress/support/shared.js|cypress/support/
cypress/support/utils.js|cypress/support/

cypress/integration/finish_mama_project/signup.spec.js|cypress/integration/
cypress/integration/finish_mama_project/articles/crud.spec.js|cypress/integration/articles/
```

- [x] Создай скрипт `download.js`

```js
const fs = require('fs');
const wget = require('node-wget');

const data = fs.readFileSync('mama_files.txt', 'utf8');
const lines = data.split("\n");

console.log(process.env.BASE_URL);

for (const line of lines) {
    if (!line) {
        continue;
    }
    const [file, dest] = line.split('|');
    const url = process.env.BASE_URL + '/' + file;
    console.log('download', url, 'to', dest);
    if (!fs.existsSync(dest)) {
        fs.mkdirSync(dest, {recursive: true});
    }
    wget({url, dest}, () => console.log('done'));
}
```

- [x] Запусти в терминале:

```bash
BASE_URL=https://raw.githubusercontent.com/breslavsky/hello-cypress/main node download.js
```

- [x] Проверь, что все файлы из `mama_files.txt` загрузились.
- [x] В фикстуру `me-user.json` пропиши свои credentials.
- [x] Проверь, что все ссылки в `README` открываются.
- [x] Прочитай и выполни все доступные тест-кейсы.

* ❓ На каком языке программирования написан этот скрипт?
* ❓ Что такое `process.env`?
* ❓ Зачем строка `if (!line)`?
* ❓ Что делает `split()`?

***

### +1.4. Готовим Cypress

- [x] Создай файл `~/cypress.json`

```diff
+     "baseUrl": "https://demo.realworld.io/",
+     "defaultCommandTimeout": 10000
```

- [x] Прогони все тесты `npx cypress run`
- [x] Исправь 🔴 ошибки в тестах.
- [x] Вспомни код и **выпиши** непонятные участки.

Сразу хочешь сбежать 🤨 в подсказки? Нет, just do it сам! ~"Мотивация"

<details>
  <summary>Что делать?</summary>

- [x] Поставь пакет [Faker](https://github.com/faker-js/faker)

```bash
npm i @faker-js/faker --save-dev
```

- [x] В файле `crud.spec.js` исправь:

```diff
- 68 | cy.get('@articlePage').find('[ng-bind-html$=markdown]')
+ 68 | cy.get('@articlePage').find('[ng-bind-html$=body]')
```

- [x] В файле `signup.spec.js` исправь:

```diff
- 19 | cy.get('@registerPage').find('form').should('be.visible').as('signupForm');
+ 19 | cy.get('@registerPage').find('form').should('be.visible').as('registerForm');
```

</details>

***

## +2. Тест глобальной ленты статей

### +2.1. Декомпозиция UI

- [x] Перейди на главную страницу приложения Conduit https://demo.realworld.io/
- [x] Ответь на вопросы: **Что я вижу? Что я могу?**
- [x] Запиши ответы в файл `~/ui/home_page.md` в формате:

```md
Данный файл содержит декомпозицию UI [домашней страницы](https://demo.realworld.io/) приложения Conduit.

# Структура UI

Как пользователь, на домашней странице:

1. Я вижу — что-то
1. Я могу — чего-то
```

***

- [x] Сверь свои ответы с эталоном:

<block>
**Как пользователь, на домашней странице:**
1. Я вижу — список **карточек** статей.
1. Я вижу — в каждой карточке **аттрибуты** статьи:
  * `created at` — дата создания статьи
  * `author` — автор статьи
    * `username` — имя пользователя
    * `avatar` — эмблема пользователя
  * `likes` — количество лайков
  * `title` — заголовок статьи
  * `description` — краткое описание статьи
  * `tags` — ключевые слова
1. Я могу — перейти на **детальную страницу** выбранной статьи.
1. Я могу — лайкнуть **выбранную** статью.
1. Я могу — **навигироваться** по списку статей используя пейджинг.
1. Я могу — фильтровать статьи в списке по **популярным** тегам.
</block>

<details>
  <summary>Откуда мы знаем **названия** аттрибутов статьи?</summary>

Аттрибуты/поля/свойства — объекта **статья** хранятся в базе данных на бекенде и отражаются на сайте.

- [x] **Проинспектируй структуру** документа в инструментах разработчика Chrome.
- [x] Найди соответствующий **вызов API** XHR-запрос на бекенд для загрузки статей.
- [x] Запроси от разработчиков **документацию** по API и структуре базе данных.

</details>

Что бы сделать декомпозицию UI — я использую принцип: Что я вижу? Что я могу? ~"В конспект"

* ❓ Что такое UI, декомпозиция и прокрастинация 😂?
* ❓ Что такое карточка в UI?
* ❓ Что такое пейджинг?

***

### +2.2. Функциональная декомпозиция

**Функция приложения** — это конкретная задача, которую выполняет программа для пользователя. ~"В конспект"

Базовые функции любого приложения: ввод, вывод, загрузка, отправка, поиск, переход, навигация и т.д.

- [x] Определи функции в `home_page.md` в формате:

```md
# Функции приложения

1. Вывод чего-то
1. Переход куда-то
1. Лайк чего-то
1. Навигация где-то используя что-то
1. Фильтрация чего-то как-то
```

***

- [x] Сверь свои ответы с эталоном:

<block>
**Функции приложения:**
1. Вывод статей в списке.
2. Переход к детальной странице статьи.
3. Лайк статьи.
4. Навигация в списке через пейджинг.
5. Фильтрация статей по тегам.
</block>

Скучно 🥱? Неинтересно 🤮? Хочется сразу бежать писать код и на это забить 😜?

> ❗ Что бы написать качественный код — нужен алгоритм! ~"В конспект"

Ты никогда не научишься писать качественный код тестов без навыка **функциональной декомпозиции** и написания тест-кейсов в ручную. ~"Мотивация"

***

### +2.3. Подготовка списка тест-кейсов

**Задача:** написать тест-кейсы для каждой функции.

Для удобства сгруппируем тесты функций в тест-сьют: **Статьи → Глобальная лента**

- [x] Создай папку  `~/test_cases/articles/global_feed`
- [x] Обнови `README`

```diff
- * [ ] global articles feed
+
+ ## Global feed
+ * [ ] display article list
+ * [ ] open article detail page
+ * [ ] like article
+ * [ ] navigate in list by paging
+ * [ ] filter articles by tag
```

***

### +2.4. Вывод статей в списке

- [x] Опиши тест-кейс — **display article list**

*** 10:00 ***

- [x] Добавь ссылку в `README`
- [x] Приведи свой тест-кейс в соответствии с [эталоном](/test_cases/articles/global_feed/display_article_list.md)
- [x] Выполни тест в ручную.
- [x] Напиши тест на Cypress используя заготовку:

```js
cy.get('?')
  .each(article => {
    cy.wrap(article).within(() => {
      // check article
    });
  });
```

*** 10:00 ***

- [x] Приведи свой код в соответствии с [эталоном](/cypress/integration/finish_mama_project/articles/global-feed.spec.js#L41)

***

### +2.5. Переход к детальной странице статьи

- [x] Опиши тест-кейс — **open article detail page**

*** 10:00 ***

- [x] Добавь ссылку в `README`
- [x] Приведи свой тест-кейс в соответствии с [эталоном](/test_cases/articles/global_feed/open_article_detail_page.md)
- [x] Выполни тест в ручную.
- [x] Напиши тест на Cypress используя заготовку:

```js
const rand = getRandomNumber(?, ?);
cy.get('?')
  // TODO: add waiting for elements
  .eq(rand)
  .as('randomArticle');
```

*** 10:00 ***

- [x] Приведи свой код в соответствии с [эталоном](/cypress/integration/finish_mama_project/articles/global-feed.spec.js#L66)

***

### +2.6. Лайк статьи

- [x] Опиши тест-кейс — **like article**

*** 10:00 ***

- [x] Добавь ссылку в `README`
- [x] Приведи свой тест-кейс в соответствии с [эталоном](/test_cases/articles/global_feed/like_article.md)
- [x] Выполни тест в ручную.
- [x] Напиши тест на Cypress используя заготовку:

```js
cy.get('?')
  .invoke('text')
  .invoke('trim')
  .then(likes => parseInt(likes))
  .as('likesBefore');

cy.get('?')
  .invoke('hasClass', '?')
  .then(likedBefore => {
      cy.get('@likesBefore').then(likesBefore => {
        const expectingLikes = likesBefore + (likedBefore ? -1 : 1);
        cy.get('?')
          .invoke('text')
          .invoke('trim')
          .then(likes => parseInt(likes))
          .should('eq', expectingLikes);
      });
  }):
```

❓ Что делает функция `parseInt`?

*** 10:00 ***

- [x] Приведи свой код в соответствии с [эталоном](/cypress/integration/finish_mama_project/articles/global-feed.spec.js#L90)

***

### +2.7. Навигация в списке через пейджинг

- [x] Опиши тест-кейс — **navigate in list by paging**

*** 10:00 ***

- [x] Добавь ссылку в `README`
- [x] Приведи свой тест-кейс в соответствии с [эталоном](/test_cases/articles/global_feed/navigate_in_list_by_paging.md)
- [x] Выполни тест в ручную.
- [x] Напиши тест на Cypress.

*** 10:00 ***

- [x] Приведи свой код в соответствии с [эталоном](/cypress/integration/finish_mama_project/articles/global-feed.spec.js#L133)

***

### +2.8. Фильтрация статей по тегам

- [x] Опиши тест-кейс — **filter articles by tag**

*** 10:00 ***

- [x] Добавь ссылку в `README`
- [x] Приведи свой тест-кейс в соответствии с [эталоном](/test_cases/articles/global_feed/filter_articles_by_tag.md)
- [x] Выполни тест в ручную.
- [x] Напиши тест на Cypress.

*** 10:00 ***

- [x] Приведи свой код в соответствии с [эталоном](/cypress/integration/finish_mama_project/articles/global-feed.spec.js#L186)
- [x] Поставь отметки, что тесты написаны в `README`

***

## +3. Тест комментариев

### +3.1. Добавление комментария

- [x] Обнови `README`

```diff
+
+ # Commenting
+ * [ ] add comment
+ * [ ] delete comment
```

- [x] Опиши тест-кейс — **add comment**

*** 10:00 ***

- [x] Добавь ссылку в `README`
- [x] Приведи свой тест-кейс в соответствии с [эталоном](/test_cases/add_comment.md)
- [x] Выполни тест в ручную.
- [x] Напиши тест на Cypress.

*** 10:00 ***

- [x] Приведи свой код в соответствии с [эталоном](/cypress/integration/finish_mama_project/commenting.spec.js#L73)

***

### +3.2. Удаление комментария

- [x] Опиши тест-кейс — **delete comment**

*** 10:00 ***

- [x] Добавь ссылку в `README`
- [x] Приведи свой тест-кейс в соответствии с [эталоном](/test_cases/delete_comment.md)
- [x] Выполни тест в ручную.
- [x] Напиши тест на Cypress.

*** 10:00 ***

- [x] Приведи свой код в соответствии с [эталоном](/cypress/integration/finish_mama_project/commenting.spec.js#L88)
- [x] Поставь отметки, что тесты написаны в `README`