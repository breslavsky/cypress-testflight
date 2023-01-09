# Туториал: фейк дата в тестах

Подойдет тем, кто хочет научиться генерировать и использовать фейковые данные.

# 👍 Что сделаем

* Узнаем про фейк данные и научимся использовать их в Cypress тестах.
* Опишем тест-кейсы в Markdown для добавления, удаления и редактирования статей в приложении блогов.
* Разберем и напишем оптимальный код с хуками, алиасами, функциями и т.д.

# 🙋‍ Перед началом

* Ты инициализировал чистый **Node.js** проект `%/projects/cypress/fake_data`
* Ты установил Cypress `npm i cypress@9 --save-dev`

***

# 🔢 Шаги

## +1. Готовим план

Возвращаемся к мама проекту [Conduit](https://demo.realworld.io/)

В `README` на [GitHub](https://github.com/gothinkster/realworld) мы нашли [спецификацию на роутинг](https://realworld-docs.netlify.app/docs/specs/frontend-specs/routing/) — это дает нам представление о структуре приложения и его функциональных возможностей.

**Задача:** составить список функциональных тестов для работы со статьями.

- [x] Создай файл `~/test_cases/README.md`
- [x] Добавь Markdown:

```markdown
This file contains test cases for [Conduit project](https://demo.realworld.io/)

# Sign up
* [x] register user
* [x] login user
* [x] logout user

# Articles 
* [ ] publish article
* [ ] delete article
* [ ] edit article
```

- [x] Открой файл в режиме просмотра.

* ❓ Чем отличается `* [ ] ...` от `* [x] ...`?
* ❓ Почему в тест-сьюте **Sign up** все тесты `[x]`?

***

## +2. Тест публикации статьи

### +2.1. Описываем тест-кейс

- [x] Найди функцию публикации статьи в приложении.

Перед тобой форма с полями:
1. **title** — заголовок статьи
1. **description** — краткое описание статьи
1. **body** — содержимое статьи в формате Markdown
1. **tags** — ключевые слова

<details>
  <summary>Как мы узнали название полей формы?</summary>

- [x] Проинспектируй поля формы в инструментах разработчика Chrome.

</details>

Данные поля описывают объект **статья** который будет сохранен в базе данных на бекенде и отражен на сайте.

Чек-лист 👇 теста публикации статьи:
1. Открыть редактор.
2. Заполнить форму.
3. Сохранить статью.
4. Проверить, что данные статьи отражаются корректно.

Напишем тест-кейс публикации статьи:

<block>
### It should do publish article:

#### Before
1. Open https://demo.realworld.io/
2. Repeat 2-9 from [login user](login_user.md)
3. Url should be `/#/` — home page

#### Open editor
4. Click **New Article** item in app header menu
5. Url should be `/#/editor/`
6. Page should have add article form

#### Fill form
7. Type `{title}` into **Title** form field
8. Type `{description}` into **Description** form field
9. Type `{body}` into **Body** form field
10. Type `{tags}` into **Tags** form field

#### Save article
11. Click on **Publish Article** button

#### Check article data
12. Url should be `/#/article/{slug}`
13. Page title should be `{title}`
14. Article body should contains `{body}` rendered Markdown
15. Article should have `{tags}`

### Where:
* `{title}` — string with length from 20 to 50 chars
* `{description}` — string with length from 20 to 255 chars
* `{body}` — string in Markdown with length from 300 to 1000 chars
* `{tags}` — list keywords separated by comma
* `{slug}` — article in url path address

### To do:
* [ ] Сlarify fields validation templates on back-end.
</block>

- [x] Переведи тест-кейс на русский язык.
- [x] Выполни тест в ручную.
- [x] Создай файл `~/test_cases/publish_article.md` из [примера](/test_cases/articles/crud/publish_article.md?plain=1)
- [x] Добавь ссылку на тест-кейс в `README.md`

* ❓ Зачем нам **To do**?

***

### +2.2. Играемся с фейками

**Задача:** заполнить поля формы.

В качестве решения мы можем:

#### 1. Захардкодить данные:

```js
const title = 'Super nice article';
cy.get('@editArticleForm').find('input[ng-model$=title]').type(title);
```

#### 2. Использовать фикстуру:

```js
import article from '/cypress/fixtures/article.json';

cy.get('@editArticleForm').find('ng-model$=title').type(article.title);
```

В обоих случаях, мы создаем статью с одними и теме же фиксированными данными. 

Однако, для успешного прохождения данного теста — это **не обязательное** условие.

> Если в тест можно добавить **вариативности** не нарушив его **стабильность** — лучше это сделать. ~"В конспект"
 
Динамические данные можно создавать добавляя **соль** — что-то уникальное.

Например, можно добавить дату или случайное число:

```js
let title = 'Super nice article from ' + new Date().toUTCString();
title = 'Super nice article with salt ' + Math.random();
```

Но есть более **трушный** способ — фейковые данные.

- [x] Установи [Faker](https://github.com/faker-js/faker) — generate fake data for testing.

```bash
npm i @faker-js/faker --save-dev
```

- [x] Создай файл `~/js_examples/faker.js` с содержимым:

```js
const { faker } = require('@faker-js/faker');

function generateFakeArticle() {
    return {
        title: faker.lorem.sentence(),
        description: faker.lorem.paragraph(),
        tags: [
            faker.word.adjective(),
            faker.word.adjective(),
            faker.word.adjective()
        ]
    };
}

const article = generateFakeArticle();
console.log('title =', article.title);
console.log('description =', article.description);
for (const tag of article.tags) {
    console.log('tag =', tag);
}
```

- [x] Выполни скрипт `node js_examples/faker.js`

***

- [x] Изучи [API библиотеки](https://fakerjs.dev/api/)
- [x] Создай много фейковых пользователей:

```js
function generateFakeUser() {
    return {
        id: '?',
        email: '?',
        firstName: '?',
        lastName: '?',
        about: '?',
        job: '?',
        company: '?',
        address: {
            avatar: '?',
            country: '?',
            city: '?',
            street: '?',
            zipCode: '?'
        }
    };
}

for (let i = 0; i <= 5; i++) {
    console.log(generateFakeUser());
}
```

***

### +2.3. Пишем код теста

- [x] Добавь фикстуру `~/cypress/fixtures/me-user.json` из [примера](/cypress/fixtures/me-user.json)
- [x] Создай файл `~/cypress/support/shared.js` из [примера](/cypress/support/shared.js)
- [x] Создай файл теста `articles.spec.js`
- [x] Напиши тест публикации статьи следуя описанию тест-кейса:
  * Используй функцию `login()` из `shared.js`
  * Используй **Faker** для заполнения формы.

*** 05:00 ***

- [x] Сверь свой код с [эталоном](/cypress/integration/fake_data/articles1.spec.js)
- [x] Разберись в каждой строчке кода мастера.
- [x] Перенеси найденные улучшения к себе.
- [x] Добавь отметку в `README.md` что тест написан.

## +3. Тест удаления статьи

### +3.1. Описываем тест-кейс

Чек-лист 👇 теста удаления статьи:
1. Опубликовать статью.
2. Найти статью.
3. Удалить статью.
4. Проверить, что статья удалена.

Напишем тест-кейс публикации статьи:

<block>

### It should delete article:

#### Before
1. Open https://demo.realworld.io/
2. Repeat 2-9 from [login user](login_user.md)
3. Url should be `/#/` — main page

#### Add article
4. Repeat 4-11 from [publish article](publish_article.md)

#### Open me profile
5. Click `{user_name}` link in app header
6. Url should be `/#@{user_name}` — user profile page

#### Find my article
7. My articles menu item should be active
8. Click on `{title}` link in articles list

#### Delete article
9. Click on **Delete article** button

#### Check article has been deleted
10. My articles list should not have `{title}`

### Where:
* `{title}` — article title added by user
* `{user_name}` — name logged-in user

</block>

- [x] Переведи тест-кейс на русский язык.
- [x] Выполни тест в ручную.
- [x] Создай файл `~/test_cases/delete_article.md` из [примера](/test_cases/articles/crud/delete_article.md?plain=1)
- [x] Добавь ссылку на тест-кейс в `README.md`

***

### +3.2. Пишем код

Для данного теста тебе потребуется повторить часть теста публикации статьи.

- [x] Чтобы избежать дублирования кода создай функцию `addArticle() → article`

```js
function addArticle() {
  // open editor
  // ...
  const article = generateFakeArticle();
  // fill and submit form
  // ...
  return article;
}
```

- [x] Отрефактори код теста публикации статьи.
- [x] Напиши тест удаления статьи следуя описанию тест-кейса:
  * Используй функцию `addArticle()`
  * Чтобы найти добавленную статью используй сниппет:

```js
const article = addArticle();

cy.get('article-list').contains(article.title)
    .parents('article-preview')
    .find('a.preview-link').click();
```

  * Чтобы определить, что статья удалена:

```js
// waiting articles are loaded
cy.get('@myArticles').find('article-preview')
    .should('have.length.greaterThan', 0);

// check article are not presented
cy.get('@myArticles').contains(article.title)
    .should('have.length', 0);
```

* ❓ Что делает `parents('?')`?
* ❓ Что делает `have.length.greaterThan`?

<details>
  <summary>`.parents()` in reels 📹</summary>

<video width="408px" height="725px" controls>
  <source src="artefacts/reels/find_link_in_card.mp4" type="video/mp4">
</video>
</details>

*** 05:00 ***

- [x] Сверь свой код с [эталоном](/cypress/integration/fake_data/articles2.spec.js)
- [x] Разберись в каждой строчке кода мастера.
- [x] Перенеси найденные улучшения к себе.
- [x] Добавь отметку в `README.md` что тест готов.

***

## +4. Тест редактирования статьи

- [x] Создай файл `~/test_cases/edit_article.md` из [примера](/test_cases/articles/crud/edit_article.md?plain=1)
- [x] Добавь ссылку на тест-кейс в `README.md`
- [x] Переведи тест-кейс на русский язык.
- [x] Выполни тест в ручную.
- [x] Напиши код теста редактирования статьи.

***

- [x] Отрефактори код всех тестов используя новые функции:
* `openMyArticles()` — открывает список моих статей.
* `openMyArticle(article)` — открывает мою статью.
* `checkArticle(article)` — проверят данные статьи.
* `clearArticle()` — очищает форму редактирования статьи.
* `fillArticle()` — заполняет форму редактирования статьи новыми фейковыми данными.

*** 10:00 ***

- [x] Сверь свой код с [эталоном](/cypress/integration/fake_data/articles3.spec.js)
- [x] Разберись в каждой строчке кода мастера.
- [x] Перенеси найденные улучшения к себе.
- [x] Добавь отметку в `README.md` что тест готов.

На этом пока все 🥳

<details>
  <summary>Посмотри 👇 насколько хороший код у тебя получился</summary>

<iframe src="https://giphy.com/embed/VhWVAa7rUtT3xKX6Cd" 
  width="480" height="360" frameBorder="0" class="giphy-embed"></iframe>
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
