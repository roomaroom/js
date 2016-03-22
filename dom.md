#Окружение: DOM, BOM и JS
Как видно из рисунка, на вершине стоит window.

У этого объекта двоякая позиция – он с одной стороны является глобальным объектом в JavaScript,
с другой – содержит свойства и методы для управления окном браузера, открытия новых окон, например:
```
// открыть новое окно/вкладку с URL http://ya.ru
window.open('http://ya.ru');
```
##Объектная модель документа (DOM)
Глобальный объект document даёт возможность взаимодействовать с содержимым страницы.
```
document.body.style.background = 'red';
alert( 'Элемент BODY стал красным, а сейчас обратно вернётся' );
document.body.style.background = '';
```
##Объектная модель браузера (BOM)
BOM – это объекты для работы с чем угодно, кроме документа.
- Объект navigator содержит общую информацию о браузере и операционной системе. Особенно примечательны два свойства: navigator.userAgent – содержит информацию о браузере и navigator.platform – содержит информацию о платформе, позволяет различать Windows/Linux/Mac и т.п.
- Объект location содержит информацию о текущем URL страницы и позволяет перенаправить посетителя на новый URL.
- Функции alert/confirm/prompt – тоже входят в BOM.
```
alert( location.href ); // выведет текущий адрес
```

#jQuery 
jQuery is a fast and concise JavaScript Library that simplifies HTML document traversing, event handling, animating, and Ajax interactions for rapid web development.
- jQuery is JavaScript.
- It’s lightweight library (32kb minified and GZIPed)
- Easy and fast HTML DOM Selection
- Built to work on all modern browsers
