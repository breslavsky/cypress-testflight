# Туториалы по ИТ навыкам

Привет, [Anton](https://t.me/breslavsky_anton) на связи 🤙

Перед тобой 👇 серия практических туториалов по авто-тестам на **Cypress**

Чистый **концентрат** — все как на работе, сразу в бой.

Я — Тимлид и **разработчик** с более чем **15-летним** опытом. 

Мне 36, живу и работаю в Берлине, и у меня есть огромное желание **делиться** знаниями.

# Мой подход

Я сторонник **проблемно-ориентированного** ~~программирования~~ обучения:
1. Выполняя **практические действия** и сталкиваясь с **проблемами** — у тебя возникают вопросы.
2. Получая ответы, ты ловишь **ага-эффекты!** Чем больше таких эффектов — тем большему ты научишься!

На сложные вопросы и **концепты** — я даю свои **расширенные** комментарии.

# +Менторство по Zoom

Каждый вторник и четверг я провожу свои **менторские онлайн стендапы** в Zoom для всех желающих.

Подробности и 🔔 анонсы новых туториалов в [Телеграмм](https://t.me/epic_one_hour)

Скринкасты и записи стендапов на 🎬[YouTube](https://www.youtube.com/@epic_one_hour)

# +Туториалы по Cypress

1. [Первый полет на Cypress](https://md.epic1h.com/cypress_test_flight)
2. [Находим лучшие селекторы](https://md.epic1h.com/best_selectors)
3. [Тестируем мама проект на Cypress](https://md.epic1h.com/test_mama_project)
4. [Мой первый рефактор в Cypress](https://md.epic1h.com/my_first_refactor)
5. [Фейк дата в тестах](https://md.epic1h.com/fake_data)
6. [Как устроен Cypress внутри](https://md.epic1h.com/deep_cypress)
7. [Заканчиваем мама проект](https://md.epic1h.com/finish_mama_project)
8. Тестирование API в Cypress
9. Обновляем Cypress до 12
10. Собираем проект локально
11. Запускаем тестирование через CI/CD в GitLab
12. Деплоим проект на своем сервере
13. Визуальное тестирование через Cypress

## Силлабус

> **Syllabus** – учебный план 😂

```mermaid
%%{ init: { 'flowchart': { 'curve': 'monotoneX' } } }%%
flowchart TB
cypress_test_flight(<span style='font-size:25px'>Первый полет</span>)
cypress_test_flight --> node_js(Node.js)
node_js --> package_json(package.json)
node_js --> npm
npm --> npm_init(npm init)
npm --> npm_install(npm install)
node_js --> node_modules
node_js --> npx
npx --> cypress_npx(cypress)
cypress_npx --> cypress_open(open)
cypress_npx --> cypress_run(run)
cypress_test_flight --> cypress(Cypress)
cypress ---> cy_visit(visit)
cypress ---> cy_get(get)
cypress ---> cy_type(type)
cypress ---> cy_click(click)
cypress ---> cy_should(should)
cy_should --> cy_should_have_text(have.text)
cypress_test_flight --> TDD
TDD ---> it

style cypress_test_flight fill:LightCoral,stroke:#333,stroke-width:4px
click cypress_test_flight "https://md.epic1h.com/cypress_test_flight" _blank
click node_js "https://youtu.be/lqqlaOuxrpM?t=136" _blank
click package_json "https://youtu.be/lqqlaOuxrpM?t=194" _blank
click npm_init "https://youtu.be/lqqlaOuxrpM?t=194" _blank
click npm_install "https://youtu.be/lqqlaOuxrpM?t=239" _blank
click cypress_open "https://youtu.be/lqqlaOuxrpM?t=287" _blank
click cy_visit "https://youtu.be/lqqlaOuxrpM?t=370" _blank
click cy_get "https://youtu.be/lqqlaOuxrpM?t=558" _blank
click cy_type "https://youtu.be/lqqlaOuxrpM?t=563" _blank
click cy_click "https://youtu.be/lqqlaOuxrpM?t=591" _blank
click cy_should "https://youtu.be/lqqlaOuxrpM?t=637" _blank
click cy_should_have_text "https://youtu.be/lqqlaOuxrpM?t=639" _blank
click cypress_run "https://youtu.be/lqqlaOuxrpM?t=708" _blank
click it "https://youtu.be/lqqlaOuxrpM?t=365" _blank
```

```mermaid
%%{ init: { 'flowchart': { 'curve': 'monotoneX' } } }%%
flowchart TB
best_selectors(<span style='font-size:25px'>Лучшие селекторы</span>)
best_selectors ---> dev_tools(DevTools)

dev_tools --> query_selector_all(querySelectorAll)
dev_tools --> $$($$)

best_selectors --> css_selectors(CSS selectors)
css_selectors --> semantic_ui(Semantic UI)
css_selectors --> data_cy("[data-cy]")

best_selectors --> tiny_web_server(Tiny Web Server)
best_selectors --> wget(Wget)

best_selectors --> js_TODO(TODO)

style best_selectors fill:LightCoral,stroke:#333,stroke-width:4px
click best_selectors "https://md.epic1h.com/best_selectors" _blank
click query_selector_all "https://youtu.be/tK2F2wNvcWI?t=1853" _blank
click $$ "https://youtu.be/tK2F2wNvcWI?t=1764" _blank
click semantic_ui "https://youtu.be/tK2F2wNvcWI?t=2000" _blank
click tiny_web_server "https://youtu.be/tK2F2wNvcWI?t=610" _blank
click wget "https://youtu.be/tK2F2wNvcWI?t=1025" _blank
click js_TODO "https://youtu.be/tK2F2wNvcWI?t=3058" _blank
```

```mermaid
%%{ init: { 'flowchart': { 'curve': 'monotoneX' } } }%%
flowchart TB
test_mama_project(<span style='font-size:25px'>Тестируем мама проект</span>)
test_mama_project --> conduit(Conduit)

conduit --> login
conduit --> register
conduit --> logout

test_mama_project --> tdd(TDD)
tdd ---> tdd_describe(describe)
test_mama_project --> java_script("Java Script")

java_script --> js_math(Math)
js_math --> js_random(random)
js_math --> js_round(round)

test_mama_project --> cypress(Cypress)
cypress --> cy_it_only(it.only)
cypress --> cy_url(url)
cypress --> cy_should(should)
cy_should --> cy_include(include)
cy_should --> cy_contain_text(contain.text)
cy_should --> cy_be_visible(be.visible)

style test_mama_project fill:LightCoral,stroke:#333,stroke-width:4px
click test_mama_project "https://md.epic1h.com/test_mama_project" _blank
```

```mermaid
%%{ init: { 'flowchart': { 'curve': 'monotoneX' } } }%%
flowchart TB
my_first_refactor(<span style='font-size:25px'>Мой первый рефактор</span>)


my_first_refactor --> cypress(Cypress)
cypress --> cypress_config(cypress.json)
cypress_config --> base_url(Base URL)

cypress --> hooks
hooks --> before_each(Before Each)
cypress --> aliases
aliases --> as
aliases --> get_alias("@")

cypress --> fixtures
fixtures --> me_user_json(me-user.json)

my_first_refactor --> signup_spec_js(signup.spec.js)
signup_spec_js --> login_me(loginMe)
my_first_refactor --> utils(utils.js)
utils --> get_random_number(getRandomNumber)

style my_first_refactor fill:LightCoral,stroke:#333,stroke-width:4px
click my_first_refactor "https://md.epic1h.com/my_first_refactor" _blank
```

# +Туториалы по ручному тестированию

1. [Ломаем приложение онлайн-банка](https://md.epic1h.com/became_a_tester)
1. [Организуем баг-трекинг в стартапе](https://md.epic1h.com/bug_tracking)
1. [Исследуем баги и пишем профессиональные баг-репорты](https://md.epic1h.com/perfect_bug_reports)

# +Менторство

1. [Java Script](https://md.epic1h.com/js_mentor)

# +Челленджы

1. [Спасти мир от хакера Hакатика](https://md.epic1h.com/save_the_world)

# +Стримы

1. [Стрим-практикум: мемы учат](https://md.epic1h.com/memes_teach)
