# CSS Users variables - Пользовательские перемененные CSS

[Определение переменных и установка значений](#variable-init)  
[Использование переменных](#using-variables)  
[Установка дефолтных значений](#set-default-value)  
[Области видимости переменных CSS](#variable-scopes)  
[Переопределение переменной для элемента](#update-value-variable)  
[Получение значений с помощью JavaScript](#get-value-variable-js)  
[Изменение значений переменной с помощью JavaScrtipt](#update-value-variable-js)  
[Используемые ресурсы](#resources)  

---
<a name="variable-init"><h2>Определение переменных и установка значений</h2></a>

Переменные задаются двойным дефисом `--`, после двоеточия устанавливается значение переменной.

```css
{
    --name-css-variable: value-variabel;
    --color-main: #2cc;
    --margin-main: 10px;
}
```

---
<a name="using-variables"><h2>Использование переменных</h2></a>

```css
{
    background-color: var(--color-main);
}
```

---
<a name="set-default-value"><h2>Установка дефолтных значений</h2></a>

Если переменная отсутствует - будут использованы дефолтные значения

```css
{
    background-color: var(--color-main, #06c);
}
```

В качестве значения для переменной могут выступать другие переменные

```css
{
    --btn-color-main: var(--color-main, var(--color-default));
}
```

>Если переменна не существует - `var(--default-variable)` функция `var()` ни чего не вернёт.

---
<a name="variable-scopes"><h2>Области видимости переменных CSS</h2></a>

По области видимости переменные делятся на
- глобальные переменные - используются в любом месте
- локальные переменные - используются для того селектора, в котором были определены

Определение глобальных переменных
```css
:root {
    --main-bg-color: #f4f4f4;
    --main-txt-color: #333;
    --container-width: 90%;
    --header-bg-color: #333;
    --header-txt-color: #fff;
}
```

Определение локальных переменных для селекторов `.box`
```css
.box {
    --box-bg-color: #ddd;
    --box-main-color: #06c;
    --box-padding: 5px 10px;
    --box-shadow-h-offset: 10px;
    --box-shadow-v-offset: 5px;
    --box-shadow-blur: 5px;
}
```

>Локальные переменные могут использоваться только для заданного селектора, и его дочерних элементов

```css
.box {
    background-color: var(--box-bg-color);
    padding: var(--box-padding);
    border: 1px solid var(--box-main-color);
    box-shadow: var(--box-shadow-h-offset) var(--box-shadow-v-offset)
    var(--box-shadow-blur) var(--box-main-color);
}

.box h2 {
    color: var(--box-main-color);
}


/* h2 будет синим цветом только в блоке .box */
h2 {
    /* то же самое что и (.box h2) - потому что 
    используются переменные из блока box */
    color: var(--box-main-color); 
}
```

```html
<h2>Заголовок с дефолтным цветом</h2>

<div class="box">
    <h2>Заголовок с переопределённым цветом</h2>
</div>
```

---
<a name="update-value-variable"><h2>Переопределение переменной для элемента</h2></a>

```css
.box p{
    --box-main-color: #555;
    color: var(--box-main-color);
}
```

>Переменная переопределена для элемента `.box p` в других местах переменная имеет старое значение.

---
<a name="get-value-variable-js"><h2>Получение значений с помощью JavaScript </h2></a>

```javascript
<script>
    // выведет все 
    const box = document.querySelector('.box');
    const boxStyles = getComputedStyle(box);
    console.log(boxStyles);
</script>
```

```javascript
<script>
    const box = document.querySelector('.box');
    const boxStyles = getComputedStyle(box); 
    const boxMainColor = boxStyles.getPropertyValue('--box-main-color');
    
    console.log(boxMainColor);
</script>
```

---
<a name="update-value-variable-js"><h2>Изменение значений переменной с помощью JavaScript</h2></a>

```javascript
<script>
    const box = document.querySelector('.box');
    const boxStyles = getComputedStyle(box); 
    const boxMainColor = boxStyles.getPropertyValue('--box-main-color');
    
    cons header = dovument.querySelector(#main-header);
    header.style.setProperty('--header-bg-color', boxMainColor);
</script>
```

---
<a name="resources"><h2>Используемые ресурсы</h2></a>

- [https://www.youtube.com/watch?v=sQUB039MG0I](https://www.youtube.com/watch?v=sQUB039MG0I) - CSS Variables Tutorial (CSS Custom Properties)
- [https://codepen.io/bradtraversy/pen/VyPNOr](https://codepen.io/bradtraversy/pen/VyPNOr) - Пример кода
