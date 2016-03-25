#DOM, BOM и JS
Сам по собі мова JavaScript не передбачає роботи з браузером.
Він взагалі не знає про HTML. Але дозволяє легко розширювати себе новими функціями і об'єктами.

![Image](https://learn.javascript.ru/article/browser-environment/windowObjects.png)
###Як видно з малюнка, на вершині стоїть window.

У цього об'єкта двояка позиція - він з одного боку є глобальним об'єктом в JavaScript,
з іншого - містить властивості та методи для управління вікном браузера, відкриття нових вікон, наприклад:
```
window.open('http://google.com');
```
##Об'єктна модель документа (DOM)
Глобальний об'єкт document дає можливість взаємодіяти з вмістом сторінки.
Кожен HTML-тег утворює вузол дерева з типом «елемент». Вкладені в нього теги стають дочірніми вузлами. Для представлення тексту створюються вузли з типом «текст».
```
document.body.style.background = 'red';
alert( 'Елемент BODY став червоним, а зараз назад повернетьсяя' );
document.body.style.background = '';
document.getElementsByTagName("p");
document.getElementById("main");
document.getElementById("demo").innerHTML = 'text';
```
http://www.w3schools.com/js/js_htmldom_eventlistener.asp

##Об'єктна модель браузера (BOM)
BOM - це об'єкти для роботи з чим завгодно, крім документа.
- Об'єкт navigator містить загальну інформацію про браузер і операційну систему. Особливо примітні два властивості: navigator.userAgent - містить інформацію про браузер і navigator.platform - містить інформацію про платформу, дозволяє розрізняти Windows / Linux / Mac і т.п.
- Об'єкт location містить інформацію про поточний URL сторінки і дозволяє перенаправити відвідувача на новий URL.
- Функції alert / confirm / prompt - теж входять в BOM.
```
screen.width;
screen.height;
location.hostname;
window.history.back();
navigator.appCodeNamenavigator.platform
navigator.platform
alert( location.href ); // выведет текущий адрес
```

#jQuery 
jQuery is a fast and concise JavaScript Library that simplifies HTML document traversing, event handling, animating, and Ajax interactions for rapid web development.
- jQuery is JavaScript.
- It’s lightweight library (32kb minified and GZIPed)
- Easy and fast HTML DOM Selection
- Built to work on all modern browsers

##Installation
Referencing to downloaded library
```
<script src="jquery.js"></script>
```
Using jQuery from other sites (e.g. Google, Microsoft, etc.)
```
<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.8.0/jquery.min.js">
</script>
```
###jQuery Philosophy
- Find some HTML
- Do something with it

###Basic syntax is: $(selector).action() :

- $ sign to define/access jQuery 
- (selector) to "query (or find)" HTML elements 
- jQuery action() to be performed on the element(s) 
```
$("p").hide();

$(document).ready(function(){
    $("p").click(function(){
        $(this).hide();
    });
});
```

#Що таке AJAX?
AJAX (абревіатура від «Asynchronous Javascript And Xml») - технологія звернення до сервера без перезавантаження сторінки.
http://www.w3schools.com/jquery/jquery_ajax_get_post.asp
