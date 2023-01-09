# Туториал: находим лучшие селекторы для UI элементов

Подойдет тем, кто хочет писать устойчивые, понятные и короткие селекторы в авто-тестах.

# 👍 Что сделаем

* Напишем тесты **регистрации** и **входа** для веб-приложения на Cypress.
* Научимся **находить** и **тестировать** селекторы через инструменты разработчика Chrome.
* Изучим **лучшие практики** и **анти-паттерны** при составлении селекторов.

# 💪 Минутка мотивации

Задача [End-To-End](https://qna.habr.com/q/401848) тестов — заставить компьютер нажимать на кнопки, вводить данные в поля формы, двигать мышкой — как это делал бы человек.

**Селекторы / локаторы** — позволяют **находить элементы** UI с которыми ты будешь **заставлять** машину взаимодействовать.

> Селекторы — **основная часть** будущего **исходного кода** твоих тестов.

От того, **насколько хорошо** ты будешь **находить селекторы** элементов, твой код будет:
* стабилен,
* понятен,
* и хорошо поддерживаться.

🤮 Твой код до:

```js
cy.get('body main div[class="panel"] form .input-primary').type('?');
cy.get('body .form #xxyyzz').type('?');
cy.get('[class="btn btn-primary"]').click();
```

🤩 Твой код после:

```js
cy.get('form.login input[name=email]').type('?');
cy.get('form.login input[name=password]').type('?');
cy.get('form.login button[type=submit]').click();
```

<iframe src="https://giphy.com/embed/vKHKDIdvxvN7vTAEOM" 
  width="480" height="400" frameBorder="0" class="giphy-embed" allowFullScreen></iframe>

# 🙋‍ Перед началом

* Ты знаешь, что такое [CSS селектор](https://developer.mozilla.org/ru/docs/Web/CSS/CSS_Selectors)
* Ты инициализировал чистый **Node.js** проект `%/projects/cypress/best_selectors`
* Ты установил Cypress `npm i cypress@9 --save-dev`

# 🫵 Наставления

**Помни:** никто тебя ничему не научит, если ты сам этого не захочешь!

* Не пропускай шаги.
* Конспектируй.
* Экспериментируй.
* **Записывай вопросы с примерами кода для стендапов с мастером.**

> Просто бывает только в рекламе! Ну ты понял в какой.

***

# 🔢 Шаги

## +1. Подготовка Веб-сервера

Тебе нужно разместить тестовое веб-приложение на локальном веб-сервере.

- [x] Установи через терминал пакет `npm install tiny-server`
- [x] В `package.json` добавь команду `start` в раздел `scripts` для запуска сервера:

```diff
  "scripts": {
+   "start": "tiny-server",
  }
```

- [x] Запусти в терминале `npm start`
- [x] Открой в **Chrome** http://localhost:3000

<details>
  <summary>Не получается 📹</summary>

<video width="600px" controls>
  <source src="assets/best_selectors/prepare_server.mp4" type="video/mp4">
</video>
</details>

* ❓ Что делает команда `npm install`?
* ❓ Зачем нужен пакет [Tiny Web Server](https://www.npmjs.com/package/tiny-server)?
* ❓ Зачем нужен раздел `scripts`?
* ❓ Что видишь в Chrome?
* ❓ Какой **веб-сервер** обработал твой HTTP запрос?

> `npm start` — это зашитая команда в **NPM**

Можно запускать команду не только `npm run start`, а короче `npm start`

📹 [Мое объяснение](https://www.youtube.com/watch?v=tK2F2wNvcWI&t=603)

***

## +2. Загрузка тестового приложения

Веб-сервер готов, нужно
скачать [тестовое приложение](https://github.com/breslavsky/hello-cypress/blob/main/apps/tesla.html) с **GitHub**.

- [x] Открой **Терминал** → **Новый терминал**
- [x] Установи пакет `npm install node-wget`
- [x] Создай папку `apps` в корне проекта.
- [x] В терминале выполни команду:

```bash
npx wget -d apps/ https://raw.githubusercontent.com/breslavsky/hello-cypress/main/apps/tesla.html
```

- [x] Проверь, что появился файл `~/apps/tesla.html`
- [x] Обнови страницу в Chrome.
- [x] В списке файлов выбери `apps/tesla.html`

> `~` — так обозначается путь до корневой папки проекта.

<details>
  <summary>Не получается 📹</summary>

<video width="600px" controls>
  <source src="assets/best_selectors/load_tesla_app.mp4" type="video/mp4">
</video>
</details>

* ❓ Что такое [wget](https://ru.wikipedia.org/wiki/Wget)?
* ❓ Что внутри файла `~/apps/tesla.html`?

<details>
  <summary>Как скачать Google 🤟</summary>

- [x] Выполни в терминале `npx wget -d google.html https://google.com/`

* ❓ В корне проекта должен появится файл `google.html`, что там?

</details>

📹 [Мое объяснение](https://www.youtube.com/watch?v=tK2F2wNvcWI&t=1018)

***

## +3. Запускаем тест приложения

Нужно открыть тестовое приложение в **Cypress**.

- [x] Создай файл `~/cypress/integration/best-selectors.spec.js`

```js
it('should do register user', () => {

    cy.visit('http://localhost:3000/apps/tesla.html');

});
```

- [x] Не забудь отформатировать код и сохранить файл!
- [x] Запусти **Cypress** командой `npx cypress open`
- [x] В **Cypress** выбери тест `best-selectors.spec.js`

<details>
  <summary>Не получается 📹</summary>

<video width="600px" controls>
  <source src="assets/best_selectors/start_test.mp4" type="video/mp4">
</video>
</details>

* ❓ Тестовое приложение открылось в Cypress?

📹 [Мое объяснение](https://www.youtube.com/watch?v=tK2F2wNvcWI&t=1397)

***

## +4. Ищем селекторы

Нужно ввести в **поле фамилия** тестовые данные.

- [x] Активируй **selector playground.**

<img class="cornered" width="200" src="assets/selector_playground.png">

- [x] Наведи на поле **фамилия** и скопируй код селектора.
- [x] Обнови код теста:

```js
it('should do register user', () => {

    cy.visit('http://localhost:3000/apps/tesla.html');
    cy.get('#b1h7e4i8d3').type('Иванов');

});
```

<details>
  <summary>Не получается 📹</summary>

<video width="600px" controls>
  <source src="assets/best_selectors/finding_selectors.mp4" type="video/mp4">
</video>
</details>

* ❓ Что пытается сделать **Cypress**?
* ❓ Почему тест не проходит?

📹 [Мое объяснение](https://www.youtube.com/watch?v=tK2F2wNvcWI&t=1553)

***

Селектор поля меняется 🥴 динамически при каждом запуске приложения.

**❗ Следует использовать устойчивые к изменениям селекторы!**

> 🙅 **Анти-паттерн**
>
> Использовать **хрупкие** селекторы, которые могут быть изменены.

Пример — [хеш](https://ru.wikipedia.org/wiki/Хеш-функция) элемента который может поменяться после новой сборки
приложения:

```html
<button id="zIyPEZ0bf">Продолжить</button>
```

> 👍 **Лучшая практика**
>
> Добавить специальные [`data-`](https://developer.mozilla.org/en-US/docs/Learn/HTML/Howto/Use_data_attributes) атрибуты к элементам в HTML разметку.

```html
<button data-cy="register">Продолжить</button>
```

В твоем тесте ты напишешь:

```js
cy.get('button[data-cy=register]').click();
```

**❗ Тестируй только то, что можешь контролировать!** ~"В конспект"

> 🙅 **Анти-паттерн**
>
> Пытаться тестировать сайт или приложение, которое ты не контролируешь.

> 👍 **Лучшая практика**
>
> Работать совместно с разработчиками сайта или приложения.


Если ты **не контролируешь** приложение, то можешь столкнуться с проблемами:

* Появится [капча](https://ru.wikipedia.org/wiki/Капча) как защита от ботов.
* Структура элементов может меняться в зависимости от неизвестных факторов.
* Твой IP просто заблокируют как бота.
* Приложение может определить, что его открыли через тестовую оболочку и не запуститься.

***

## +5. Поиск лучшего селектора

- [x] Через **selector playground** найди селекторы для:
    * Элемента с текстом **Все права защищены**.
    * Кнопки **Сбросить** на форме регистрации.

* ❓ Это хорошие селекторы?
    * `body > :nth-child(1) > :nth-child(4)`
    * `#k9b1c2e4b1 > [data-cy="reset"]`

***

Это плохие селекторы, встроенный **selector playground** в **Cypress** не справляется — в топку 🤮

### Инструменты разработчика

Всегда ищи селекторы через [Инструменты разработчика в Chrome](https://www.youtube.com/watch?v=LDJMfzTlkSI)

В окне тестового приложения:

- [x] Нажми правой кнопкой мышки на любом элементе, например кнопке войти.
- [x] Выбери из контекстного меню **Просмотр кода элемента**.

* ❓ Что ты видишь справа и слева?

***

> С помощью тэгов **HTML** и стилей **CSS** рендерится пользовательский интерфейс.

### Лучший селектор:

1. Не изменяемый — **устойчивый** к обновлениям приложения.
2. Понятный — можно прочитать на **естественном** языке:

```js
// first name input field on registration form
cy.get('form.registration input[name=first_name]')
```

3. Короткий — задействует как можно **меньше элементов** и их атрибутов в иерархии.

📹 [Мое объяснение](https://www.youtube.com/watch?v=tK2F2wNvcWI&t=1980)

***

## +6. Тест формы регистрации

Нужно написать позитивный тест-кейс **зарегистрироваться** с шагами:

1. Заполнить поле **Имя**
2. Заполнить поле **Фамилию**
3. Заполнить поле **Email**
4. Заполнить поле **Пароль**
5. Нажать кнопку **Продолжить**

* ❓ Какой селектор использовать для поля **Имя**?

> Нужно найти уникальный семантический атрибут или класс для привязки к элементу.

* Для тегов `<input>` внутри одной формы атрибуты `name=xyz` являются уникальными.
* Для тегов `<button>` атрибут `type=reset` и `type=submit` определяет семантику действия.

В нашем случае для поля **Имя** это `input[name=first_name]`

***

- [x] Для проверки селектора переключись на **Консоль**.
- [x] В строку запроса введи `$$('input[name=first_name]')` и нажмите `ENTER ↵`

<details>
  <summary>Не получается 📹</summary>

<video width="600px" controls>
  <source src="assets/best_selectors/test_registration_form.mp4" type="video/mp4">
</video>
</details>

* ❓ Найден 1 элемент? **Селектор уникален.**

***

- [x] Обнови в код теста:

```js
cy.get('input[name=last_name]').type('Иванов');
cy.get('input[name=first_name]').type('Иван');
```

* ❓ Теперь в **Cypress** тест проходит?

***

- [x] Аналогично найди селекторы и заполни поле **Email**

* ❓ Сколько найдено элементов для поля **Email**?

`$$('input[name=email]')` — cелектор для поля **Email** не уникален!

На странице 2 формы **Регистрация** и **Вход** и на каждой из них есть поле **Email**.

* ❓ Что делать когда семантический селектор не уникален? Нужно добавить **Контекст**.

### Контекст для элемента

**Контекст** для элемента: форма, группа, раздел — некоторая уникальная область интерфейса.

<img class="cornered" width="634" height="382" src="assets/best_selectors/semantic_ui.png">

### Как найти контекст

* Ищи в иерархии элемента [семантические](https://html5css.ru/html/html5_semantic_elements.php) тэги `<form>`
  , `<fieldset>`, `<header>`, `<footer>`, `<nav>` т.д.
* Не смог? Ищи **НЕ семантические** теги: `<div>`, `<span>`, `<p>` с семантическими **атрибутами** или классами.

Примеры хороших 👍 контекстов:

* `aside[data-type=left]` — ищем боковую панель слева.
* `form.registration` — маловероятно, что на одной странице 2 формы регистрации.
* `#registration` — уникальный ID элемента.
* `.registration` — семантически класс `registration` уникален.
* `[data-type=registration]` — специальный `data-*` атрибут добавленный разработчиками.
* `.app-header .app-userbar` — префикс `.app-*` в имени класса делает элементы уникальными.

Примеры плохих 🙅 контекстов:

* `aside` — в приложении может быть 2 панели: справа и слева.
* `form` — на одной странице может быть несколько форм.
* `.header` — семантически класс не уникален.
* `fieldset[name=credentials]` — на форме могут быть 2 формы с одинаковой группой полей.

**🔥 Необходимо добавлять контекст к селекторам элементов!**

Примеры хороших 👍 селекторов с контекстами:

* `form.registration input[name=first_name]` — конкретное поле на конкретной форме.
* `form[name=registration] button[type=submit]` — кнопка с конкретным поведением на форме.
* `form[name=registration] button.register` — уникальная кнопка на форме.
* `aside[data-type=left] .menu a[href="/register"]` — в левой панели в меню ссылка на конкретный адрес.

Примеры плохих 🙅 селекторов с контекстами:

* `form.registration input[type=text]` — полей с типом текст может быть много.
* `form[name=registration] button` — что делает кнопка?

- [x] Найди **контекст** для всех полей формы и обнови код теста.
- [x] Сверь свой исходный код с [эталоном](/cypress/integration/best-selectors.spec.js)

***

## +7. Тест формы входа

- [x] Напиши тест **should do login user**.
- [x] Сверь свой исходный код с [эталоном](/cypress/integration/best-selectors.spec.js)

***

## +8. Селектор по contains

Элементы в **Cypress** можно находить еше по текстовому содержимому тегов.

- [x] Замени селектор `cy.get('form.login button[type=submit]')` на `cy.contains('Войти')`

* ❓ Тест успешно пройден?

- [x] Переключи язык приложения добавлением параметра `lang=en` в URL:

```js
cy.visit('http://localhost:3000/apps/tesla.html?lang=en');
```

* ❓ Тест больше не проходит, почему?

📹 [Мое объяснение](https://www.youtube.com/watch?v=tK2F2wNvcWI&t=2950)

***

## +9. TODO для разработчиков

❗ Что делать, если нельзя найти хороший селектор:
1. Использовать **лучший** из худших.
2. Поставить **задачу разработчикам** на добавление атрибута `data-cy`

Текущая разметка:

```html
<body>
<div>
    <footer>
        <p>Все права защищены</p>
    </footer>
</div>
<body>
```

В твоем тесте:

```js
it('should do check copyrights', () => {

    // TODO: улучшить селектор footer [data-cy=copyrights]
    // временно используем contains
    cy.contains('Все права защищены').should('be.visible');
    // или строгую иерархию
    cy.get('body > div > footer p').should('have.text', 'Все права защищены.');

});
```

- [x] Зайди как разработчик в `~/apps/tesla.html` и добавь `data-cy` аттрибут:

```html
<body>
<div>
    <footer>
        <p data-cy="copyrights">Все права защищены</p>
    </footer>
</div>
<body>
```

- [x] Обнови селектор в тесте:

```js
cy.get('footer [data-cy=copyrights]').should('have.text', 'Все права защищены.');
```

> Названия аттрибутов для целей тестирования могут быть разными: 
>
> `data-for-test`, `data-ui-id`, `data-test-id` и т.д.

***

Та да 🥳 Ты дошел до конца.

# 👨‍🎓 Чему ты научился

```mermaid https://raw.githubusercontent.com/breslavsky/hello-cypress/main/syllabus/best_selectors.mm

```

# 😭 Домашка

Найди **лучшие селекторы** для [формы регистрации](https://demo.realworld.io/#/register) и заполни ниже:

1. поле имя пользователя — <md-placeholder value=".auth-page form input[ng-model$=username]"></md-placeholder>
2. поле email — <md-placeholder value=".auth-page form input[ng-model$=email]"></md-placeholder>
3. поле пароль — <md-placeholder value=".auth-page form input[ng-model$=password]"></md-placeholder>
4. кнопка регистрации — <md-placeholder value=".auth-page form button[type=submit]"></md-placeholder>

📹 [Мой разбор](https://www.youtube.com/watch?v=tK2F2wNvcWI&t=3893)

# 📹 Видео-ответы

1. [Зачем тестировщику доступ к исходному коду проекта?](https://www.youtube.com/watch?v=88CHSU2iI7M&t=381&list=PL1W_vbf7JRLDqwf56BkD44yGYbtDaK9Ak)
2. [Какие еще навыки должны быть у тестировщика?](https://www.youtube.com/watch?v=88CHSU2iI7M&t=519&list=PL1W_vbf7JRLDqwf56BkD44yGYbtDaK9Ak)
3. [Почему при обучении важно вести собственные конспекты?](https://www.youtube.com/watch?v=88CHSU2iI7M&t=942&list=PL1W_vbf7JRLDqwf56BkD44yGYbtDaK9Ak)
4. [Почему можно тестировать только то, чем можно управлять?](https://www.youtube.com/watch?v=tK2F2wNvcWI&t=475&list=PL1W_vbf7JRLDqwf56BkD44yGYbtDaK9Ak)
5. [Как скачать Google?](https://www.youtube.com/watch?v=tK2F2wNvcWI&t=1265&list=PL1W_vbf7JRLDqwf56BkD44yGYbtDaK9Ak)
6. [Какими должны быть селекторы в авто-тестах?](https://www.youtube.com/watch?v=tK2F2wNvcWI&t=1716&list=PL1W_vbf7JRLDqwf56BkD44yGYbtDaK9Ak)
7. [Что делает функция $$ в инструментах разработчика?](https://www.youtube.com/watch?v=tK2F2wNvcWI&t=1811&list=PL1W_vbf7JRLDqwf56BkD44yGYbtDaK9Ak)
8. [Какой основной алгоритм для поиска селекторов?](https://www.youtube.com/watch?v=tK2F2wNvcWI&t=1999&list=PL1W_vbf7JRLDqwf56BkD44yGYbtDaK9Ak)
9. [Что такое ага-эффект?](https://www.youtube.com/watch?v=tK2F2wNvcWI&t=3299&list=PL1W_vbf7JRLDqwf56BkD44yGYbtDaK9Ak)
10. [Какие атрибуты добавлять к элементам для улучшения селекторов?](https://www.youtube.com/watch?v=tK2F2wNvcWI&t=3524&list=PL1W_vbf7JRLDqwf56BkD44yGYbtDaK9Ak)
11. [Что такое CSS селектор по атрибуту?](https://www.youtube.com/watch?v=tK2F2wNvcWI&t=4409&list=PL1W_vbf7JRLDqwf56BkD44yGYbtDaK9Ak)
12. [Как комбинировать CSS селекторы?](https://www.youtube.com/watch?v=tK2F2wNvcWI&t=4635&list=PL1W_vbf7JRLDqwf56BkD44yGYbtDaK9Ak)
13. [Какие самые распространенные CSS селекторы?](https://www.youtube.com/watch?v=tK2F2wNvcWI&t=4742&list=PL1W_vbf7JRLDqwf56BkD44yGYbtDaK9Ak)
14. [Как красиво оформлять сообщения в Telegram?](https://www.youtube.com/watch?v=tK2F2wNvcWI&t=4960&list=PL1W_vbf7JRLDqwf56BkD44yGYbtDaK9Ak)
14. [Как правильно оформлять вопросы в Telegram?](https://www.youtube.com/watch?v=88CHSU2iI7M&t=1144&list=PL1W_vbf7JRLDqwf56BkD44yGYbtDaK9Ak)
16. [Что такое Markdown и зачем он в ИТ?](https://www.youtube.com/watch?v=tK2F2wNvcWI&t=5128&list=PL1W_vbf7JRLDqwf56BkD44yGYbtDaK9Ak)

# Артефакты

* [Селекторы CSS и их применение в автоматизации тестирования](https://habr.com/ru/company/otus/blog/350368/)
* [Все типы CSS селекторов](https://www.w3schools.com/cssref/css_selectors.asp)
* [Лучшие практики Cypress на официальном сайте](https://docs.cypress.io/guides/references/best-practices)
* [CSS и XPath для QA](https://habr.com/ru/company/skyeng/blog/588282/)
