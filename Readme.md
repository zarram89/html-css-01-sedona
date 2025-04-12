# Личный проект «Sedona»

---

_Не удаляйте и не обращайте внимание на файлы:_<br>
_`.editorconfig`, `.gitattributes`, `.gitignore`, `Contributing.md`, `Readme.md`._

---

### Памятка

#### 1.

Контентная векторная графика в разметке должна иметь атрибут role="img" и описание изображения в атрибуте aria-label.

Правильно
Контентная векторная графика имеет `role="img"` и `aria-label`.

```html
<svg
  class="logo"
  xmlns="http://www.w3.org/2000/svg"
  viewBox="0 0 140 18"
  width="367"
  height="152"
  role="img"
  aria-label="Барбершоп «Бородинский»">
    <path d="M78.55 0h-2.8v15.78h2.8V0zM91.02z"/>
</svg>
```

Текста, доступно скрытого классом visually-hidden, достаточно для описания ссылки. В макете есть только иконка.

```html
<a class="tg-icon" href="https://t.me/htmlacademy">
	<span class="visually-hidden">Канал в Telegram</span>
</a>
```
```css
.tg-icon::before {
	content: url("../images/tg.svg");
}
```

### Правильно подключить шрифт одного семейства, но разного начертания

```css
@font-face {
  font-family: "Roboto"; /* указываем во всех подключениях одно название семейства */
  font-weight: 400;
  font-style: normal;
  src: url("roboto.woff2") format("woff2"),
       url("roboto.woff") format("woff");
}

@font-face {
  font-family: "Roboto";
  font-weight: 400;
  font-style: italic;
  ...
}

@font-face {
  font-family: "Roboto";
  font-weight: 700;
  font-style: normal;
  src: url("robotobold.woff2") format("woff2"),
       url("robotobold.woff") format("woff");
}

@font-face {
  font-family: "Roboto";
  font-weight: 700;
  font-style: italic;
  ...
}
```

Используем их в css:

```css
body {
  font-family: "Roboto", "Arial", sans-serif;
  font-weight: 400;
  font-style: normal;
}

.title { /* создаём жирный заголовок */
  font-weight: 700;
}

.text-italic { /* создаём наклонный текст */
  font-style: italic;
}

.text-bold-italic { /* создаём жирный наклонный текст */
  font-style: italic;
  font-weight: 700;
}

```

При выгрузке векторной графики важно убедиться, что выгрузились именно векторные формы, описанные точками, а не тег <text>, в который обёрнуты буквы и приписаны стили.

<!-- Пример с векторными формами внутри изображения -->
```html
<svg width="106" height="41" viewBox="0 0 106 41" fill="none" xmlns="http://www.w3.org/2000/svg">
  <path d="M34.7969 20.1797C34.7969 22.0651 34.2734 … 19.7891Z" fill="black"/>
</svg>
```
```html
<!-- Пример с текстом внутри векторного изображения -->
<svg xmlns="http://www.w3.org/2000/svg">
  <style>
    .dollytext {
      font-family: "Open Sans", sans-serif;
      font-size: 16px;
    }
  </style>
  <text x="10" y="100" class="dollytext">
    DOLLY
  </text>
</svg>
```

Это слайд под главным меню. Поверх изображения наложен текст, набранный разными декоративными шрифтами. Если эти шрифты больше нигде на странице не используются, то картинку следует объединить со шрифтами в единое растровое изображение


```html
<!-- Раз это картинка, с которой нельзя скопировать текст, и её содержание ускользнёт от ридеров и роботов, стоит написать для неё визуально или скрытый текст, или хороший `alt` -->

<img src="img/some-pic.jpg" alt="Выход из зоны комфорта: то, что нам советуют. Но нельзя выйти оттуда, куда ты ещё не входил">

Или

<p class="visually-hidden">Выход из зоны комфорта: то, что нам советуют. Но нельзя выйти оттуда, куда ты ещё не входил</p>

```

Вариант: можно задать отступ всем дочерним элементам, кроме последнего.
```css
.item:not(:last-child) {
  margin-bottom: 20px;
}
```

При вставке изображения под картинкой остается небольшой отступ. В большинстве случаев этого даже не видно, так как отступ действительно небольшой, и если нет фона, то погрешность в несколько пикселей просто остаётся незаметна. Но этот отступ необходимо убрать.
Откуда берётся этот отступ? Дело в том, что по спецификации тег `img`, как это ни странно, — строчный элемент, и поэтому к нему применяется свойство `vertical-align`. В браузерах строчные элементы выравниваются по базовой линии (baseline), а пустое пространство — это пространство под выносной элемент букв (например, под нижние хвостики букв р или у).

Избавиться от отступа под изображением очень просто: нужно сменить способ отображения элемента и задать изображению свойство `display: block`.

#### Общие правила
- Сбрасывайте браузерные стили по умолчанию.
- Задавайте текстовым элементам нижний отступ.
- Не забывайте сбрасывать отступ у последнего элемента.
- Изображениям, с помощью класса, изменяйте блочную модель:

Укажем, как шрифт будет отображаться: пропишем значение swap, чтобы шрифт не блокировался и имел бесконечный период подмены. Это самое частое значение для font-display, но это не значит, что другие плохие.

#### Sticky-footer

```css
html {
  height: 100%;
}

body {
  margin: 0;
  display: flex;
  flex-direction: column;
  min-height: 100%;
}

.main-container {
  flex-grow: 1;
}

Если есть промежуточный `page-container`, то:
1. `min-height: 100%;` на родительском флекс контейнере
2. `height: 100%;` наостальных предках `html`, `body`
3. `flex-grow: 1;` для `main`

```

#### Обводка

```.container {
  outline: 5px solid black;
  outline-offset: -5px;
}
```
