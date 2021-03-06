# НАЧАЛО РАБОТЫ С NODE.JS

Мы начнем с основ — никаких предварительных знаний Node.js не требуется. Цель этой книги — начать работу с Node.js и убедиться, что вы понимаете, как писать приложение с использованием этой платформы.

В первой главе вы узнаете, что такое Node.js, как установить её на свой компьютер и как начать с ней работать — так что в следующих можно приступить к реальной разработке. Давайте начнем!

## Node.js в двух словах

![](http://blog-assets.risingstack.com/2016/Mar/node_js_logo_in_node_hero_getting_started_tutorial-1458726703612.png)
*Официальное лого Node.js*

*Node.js — это среда выполнения JavaScript, построенная на JavaScript-движке V8 из Chrome. В основе Node.js лежит **событийно-управляемая модель с неблокирующими операциями I/O**, что делает её легкой и эффективной.*

Другими словами: Node.js предлагает вам возможность писать серверный код с использованием JavaScript с невероятной производительностью. Как говорится в официальном заявлении: Node.js — это среда выполнения, в которой используется тот же  Javascript-движок V8, который вы можете найти в браузере Google Chrome. Но этого недостаточно для успеха Node.js. В Node.js используетсяlibuv, кросс-платформенная библиотека поддержки с акцентом на асинхронный ввод-вывод.

![](http://blog-assets.risingstack.com/2016/Mar/libuv_logo_in_node_hero_getting_started_tutorial-1458726737329.png)
*Официальное лого libuv*

С точки зрения разработчика, Node.js является однопоточным, но под капотом **libuv использует треды, события файловой системы, реализует цикл событий, включает в себя тред-пулинг** и так далее. В большинстве случаев вы не будете взаимодействовать с libuv напрямую.

## Установка Node.js для того, чтобы начать

Последнюю версию Node.js вы можете найти на официальном сайте: [https://nodejs.org/en/download/](https://nodejs.org/en/download/).

При таком подходе довольно легко начать работу — однако если позже по дороге вы хотите добавить больше версий Node.js в систему, лучше начать использовать nvm, диспетчер версий Node.js (Node Version Manager).

После его установки вы сможете использовать очень простой CLI API для смены версии Node.js:

**Установка различных версий Node.js**

```
nvm install 4.4
```

Затем, если вы хотите проверить в работе экспериментальную версию:

```
nvm install 5
```

Чтобы убедиться, что у вас установлена и запущена Node.js, выполните:

```
node --version
```

Если все в порядке, эта команда вернет номер версии текущего активного бинарного файла Node.js.

## Использование нескольких версий Node.js

Если вы работаете над проектом, поддерживающим Node.js v4, вы можете начать использовать эту версию с помощью следующей команды:

```
nvm use 4
```

Затем вы можете переключиться на Node.js v5 с помощью той же самой команды:

```
nvm use 5
```

---

**Хорошо, теперь мы знаем, как устанавливать Node.js и переключаться между её версиями — но в чём смысл?**

С тех пор как был сформирован Node.js Foundation, Node.js имеет план релизов. Это очень похоже на другие проекты Linux Foundation. Это означает, что есть два релиза: стабильный релиз и
экспериментальный. В Node.js стабильными версиями с долговременной поддержкой (LTS) являются те, которые начинаются с четных чисел (4, 6, 8, ...). Экспериментальные версии нумеруются нечетными числами (5, 7, ...).
Мы рекомендуем использовать версию LTS в продакшене и пробовать новые вещи с экспериментальной версией.

*Если вы используете Windows, здесь можно скачать альтернативу для nvm: [nvm-windows](https://github.com/coreybutler/nvm-windows).*

## Hello World

Чтобы начать работу с Node.js, давайте попробуем её в консоли! Запустите Node.js, просто набрав `node`:

```
$ node
>
```

Хорошо, давайте попробуем что-то напечатать:

```
$ node
> console.log(‘hello from Node.js’) 
```

После нажатия Enter вы получите следующее:

```
> console.log(‘hello from Node.js’)
hello from Node.js
undefined
```

Не стесняйтесь играть с Node.js с помощью этого интерфейса — я обычно тестирую небольшие фрагменты кода здесь, если я не хочу помещать их в файл.

---

Пришло время создать наше приложение Hello Node.js!

Начнем с создания файла `index.js`. Откройте свою IDE (Atom, Sublime, Code — выбор за вами), создайте новый файл и сохраните его с именем `index.js`. Если вы закончили с этим, скопируйте следующий фрагмент в этот файл:

```
// index.js
console.log(‘hello from Node.js’)
```

Чтобы запустить этот файл, вы должны снова открыть свой терминал и перейти в каталог, в котором вы разместили index.js.

Как только вы успешно переместитесь в нужное место, запустите файл, используя команду `node index.js`. Вы увидите, что эта команда будет выдавать тот же результат, что и раньше, распечатывая строку непосредственно в терминале.

## Модульность для вашего приложения

Теперь у вас есть файл `index.js`, поэтому пришло время повысить уровень в вашей игре! Давайте создадим что-то более сложное, разделив наш исходный код на несколько JavaScript-файлов с целью удобочитаемости и поддерживаемости. Чтобы начать работу, вернитесь в свою IDE (Atom, Sublime, Code — выбор за вами) и создайте следующую структуру каталогов (с пустыми файлами), но пока не трогайте `package.json`, мы сгенерируем его автоматически на следующем шаге:

```
├── app
| ├── calc.js
| └── index.js
├── index.js
└── package.json
```

Каждый проект Node.js начинается с создания файла `package.json` — вы можете думать о нем как о JSON-представлении приложения и его зависимостей. Он содержит имя вашего приложения, автора(вас) и все зависимости, необходимые для запуска приложения. Мы рассмотрим раздел зависимостей позже в главе «Использование NPM».

Вы можете интерактивно генерировать файл `package.json` с помощью команды `npm init` в терминале. После запуска команды вас попросят ввести некоторые данные, например имя вашего приложения, версию, описание и так далее. Не нужно беспокоиться, просто нажимайте enter, пока не получите сформированный JSON, и вопрос `is it ok?`. Нажмите Enter в последний раз и вуаля, ваш `package.json` был автоматически сгенерирован и помещен в папку вашего приложения. Если вы откроете этот файл в своей IDE, он будет очень похож на фрагмент кода ниже.

```javascript
// package.json 
{
  “name”: “@risingstack/node-hero”,
  “version”: “1.0.0”,
  “description”: “”,
  “main”: “index.js”,
  “scripts”: {
    “test”: “echo \”Error: no test speci ed\” && exit 1”, 
    “start”: “node index.js”
  },
  “author”: “”, “license”: “ISC”
}
```

Хорошей практикой является добавление стартового скрипта в ваш пакет `package.json` — как только вы это сделаете, как показано в примере выше, вы можете запустить приложение с помощью команды `npm start`. Это очень удобно, когда вы хотите развернуть свое приложение у PaaS-провайдера — они могут распознать команду `start` и запустить приложение, используя это.

Теперь давайте вернемся к первому созданному вами файлу под названием `index.js`. Я рекомендую сохранить этот файл очень  компактным — только подключение самого приложения (файл `index.js` из подкаталога `/app`, который вы создали ранее). Скопируйте следующий код в свой файл `index.js` и нажмите «сохранить»:

```javascript
// index.js
require(‘./app/index’)
```

Теперь пришло время приступить к созданию реального приложения. Откройте файл `index.js` из папки `/app`, чтобы создать очень простой пример: добавление массива чисел. В этом случае файл `index.js` будет содержать только числа, которые мы хотим добавить, а логика, которая требует вычислений, должна быть помещена в отдельный модуль.

Вставьте этот код в файл `index.js` в каталоге `/app`.

```javascript
// app/index.js
const calc = require(‘./calc’)
const numbersToAdd = [
    3,
    4,
    10,
    2
]

const result = calc.sum(numbersToAdd)
console.log(`The result is: ${result}`)
```

Теперь вставьте фактическую бизнес-логику в файл `calc.js`, который можно найти в той же папке.

```javascript
// app/calc.js
function sum (arr) {
    return arr.reduce(function(a, b) {
        return a + b
    }, 0)
}

module.exports.sum = sum
```

Чтобы проверить, всё ли вы сделали правильно, сохраните эти файлы, откройте терминал и введите `npm start` или `node index.js`. Если вы все сделали правильно, вы получите ответ: 19. Если что-то пошло не так, внимательно просмотрите лог в консоли и найдите проблему на основе этого.

---

В следующей главе под названием «Использование NPM» мы рассмотрим, как использовать NPM, менеджер пакетов для JavaScript.
