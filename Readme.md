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
