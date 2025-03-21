# Вопросы для собеседования junior-фронтенд разработчика

## 1. Верстка (HTML, CSS, адаптивность)

**1. Какой элемент HTML5 используется для выделения главного содержимого страницы?**  
✅ `<main>` — он обозначает основной контент страницы, который уникален для данного документа.

**2. Какие способы центрирования блока по горизонтали и вертикали в CSS вы знаете?**  
✅ Несколько вариантов:
- `flexbox`: `display: flex; justify-content: center; align-items: center;`
- `grid`: `display: grid; place-items: center;`
- `position: absolute`: `top: 50%; left: 50%; transform: translate(-50%, -50%);`
- `margin: auto` (если задана ширина и высота, но только по горизонтали).

**3. Как работает `flex-grow`?**  
✅ `flex-grow` определяет, сколько свободного места займет элемент относительно других элементов. Если у одного элемента `flex-grow: 2;`, а у другого `flex-grow: 1;`, то первый займет в два раза больше свободного пространства.

**4. В чем разница между `em`, `rem` и `%` в CSS?**  
✅ 
- `em` — зависит от размера шрифта родителя.
- `rem` — зависит от размера шрифта `html`.
- `%` — зависит от родительского элемента (не только в шрифте, но и в ширине/высоте).

**5. Как сделать адаптивную верстку без медиазапросов?**  
✅ Можно использовать `flex-wrap`, `grid-template-columns: auto-fit`, `clamp()`, `min()`, `max()` и относительные единицы (`vw`, `%`).

---

## 2. JavaScript (ES6+)

**1. Как работает замыкание в JavaScript? Приведите пример.**  
✅ Замыкание — это функция, которая "запоминает" свою область видимости, даже если вызывается вне нее.

Пример:
```js
function createCounter() {
  let count = 0;
  return function () {
    count++;
    console.log(count);
  };
}

const counter = createCounter();
counter(); // 1
counter(); // 2
```
Функция внутри сохраняет доступ к `count`, даже после выхода из `createCounter()`.

**2. Что произойдет, если вызвать `console.log(a)` до объявления `let a = 10`?**  
✅ Будет ошибка `ReferenceError: Cannot access 'a' before initialization`, так как `let` (и `const`) попадают в "временную мертвую зону" (TDZ) до их объявления.

**3. Чем `==` отличается от `===` в JavaScript?**  
✅ `==` выполняет приведение типов (`"5" == 5` → `true`), а `===` сравнивает без приведения типов (`"5" === 5` → `false`).

**4. Как работает `setTimeout` внутри цикла `for`?**  
✅ `setTimeout` не останавливает цикл, он просто ставит функцию в очередь. Например:
```js
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1000);
}
// Выведет: 3, 3, 3 (из-за области видимости var)
```
Если заменить `var` на `let`, то каждое замыкание получит свою копию `i`, и результат будет `0, 1, 2`.

**5. Что делает `Array.prototype.map()` и как он отличается от `forEach()`?**  
✅ `map()` создает новый массив, а `forEach()` просто перебирает элементы, ничего не возвращая.

Пример:
```js
const nums = [1, 2, 3];
const doubled = nums.map(n => n * 2); // [2, 4, 6]
nums.forEach(n => console.log(n * 2)); // Просто выведет 2, 4, 6, но не создаст новый массив
```

---

## 3. React.js (основы, хуки, состояние)

**1. Что такое React-хуки? Почему `useState` нельзя вызывать внутри условий?**  
✅ React-хуки — это специальные функции (`useState`, `useEffect` и др.), которые позволяют работать с состоянием и жизненным циклом в функциональных компонентах.
`useState` нельзя вызывать внутри условий, потому что React использует порядок вызова хуков для их управления. Если условие изменит порядок, React собьется.

**2. Как работает `useEffect`?**  
✅ `useEffect(() => {}, [])` выполняется один раз при монтировании.
✅ `useEffect(() => {}, [someState])` срабатывает при изменении `someState`.

**3. Как передать данные от родителя к дочернему компоненту?**  
✅ Через `props`:
```jsx
function Child({ name }) {
  return <p>Привет, {name}!</p>;
}
function Parent() {
  return <Child name="Андрей" />;
}
```

**4. Что такое `React.memo`?**  
✅ Это функция, предотвращающая ненужные перерисовки компонента, если `props` не изменились.

**5. Как избежать бесконечного ререндера в `useEffect`?**  
✅ Не изменять состояние внутри `useEffect`, зависящего от этого же состояния. Можно использовать `if` или `useRef` для контроля.

---

## 4. Инструменты разработки

**1. Как отменить последний коммит в Git, но оставить изменения в файлах?**  
✅ `git reset --soft HEAD~1`

**2. Какой файл в проекте отвечает за сборку в Webpack?**  
✅ `webpack.config.js`

**3. Чем `npm` отличается от `yarn`?**  
✅ `yarn` быстрее скачивает зависимости за счет параллельной загрузки.

**4. Как работает `package-lock.json`?**  
✅ Фиксирует версии зависимостей для повторяемости сборки.

**5. Как настроить ESLint для React-проекта?**  
✅ `npm install eslint eslint-plugin-react eslint-config-airbnb --save-dev`

---

## 5. Soft Skills

**1. Как вежливо указать на ошибку в коде коллеги?**  
✅ "Можно улучшить: здесь возможен баг, если `someVar` будет `null`. Можно использовать `??`."

**2. Как подходить к изучению новой технологии?**  
✅ 1. Документация  
2. Практика  
3. Статьи, видео, курсы

**3. Что делать, если задача непонятна?**  
✅ Задать уточняющие вопросы.

**4. Как реагировать на критику кода?**  
✅ Не принимать на личный счет, рассматривать как возможность улучшить код.

**5. Как решать конфликты в команде?**  
✅ Обсудить варианты, выбрать лучший, аргументировать решения.
