#створення об'єктів
```
o = new Object();
o = {}; 
```
Об'єкт може містити в собі будь-які значення, які називаються властивостями об'єкта
```
var person = {};
person.name = 'Вася';

person.age = 25;
alert( person.name + ': ' + person.age );

var person = {
  name: "Василь",
  age: 25
};

```
```
delete person.age;
```
Іноді буває потрібно перевірити, чи є в об'єкті властивість з певним ключем..

Для цього є особливий оператор: "in".
```
if ("name" in person) {
  alert( "Властивість name існує!" );
}
alert( person.lalala === undefined );
```
##доступ через квадратні дужки
```
var person = {};
person['name'] = 'Вася'; // це саме що person.name = 'Вася'
```
##Доступ до властивості через змінну
```
var person = {};
person.age = 25;
var key = 'age';

alert( person[key] ); // виведе person['age']
```
##Назви властивостей можна перераховувати як в лапках, так і без
```
var menuSetup = {
  width: 300,
  'height': 200,
  "мама мыла раму": true
};
```
##Як значення можна тут же вказати і інший об'єкт:
```
var user = {
  name: "Таня",
  age: 25,
  size: {
    top: 90,
    middle: 60,
    bottom: 90
  }
}

alert(user.size.top);
```

##Об'єкти: перебір властивостей
##for..in
```
for (key in obj) {
  /* ... робити щось з obj[key] ... */
}
var menu = {
  width: 300,
  height: 200,
  title: "Menu"
};

for (var key in menu) {
  // цей код буде викликаний для кожного властивості об'єкта

  alert( "Ключ: " + key + " значення: " + menu[key] );
}
```
##Копіювання за значенням
Звичайні значення: рядки, числа, булеві значення, null / undefined при присвоєнні змінних копіюються цілком
```
var message = "Привіт";
var phrase = message;
```
![Image] (https://learn.javascript.ru/article/object-reference/variable-copy-value.png)
##Копіювання за посиланням
```
var user = { name: "Вася" }; 

var admin = user; 
```
![Image](https://learn.javascript.ru/article/object-reference/variable-copy-reference.png)
При копіюванні змінної з об'єктом - копіюється ця посилання, на об'єкт, як і раніше залишається в єдиному екземплярі.
```
admin.name = 'Петро'; // поміняли дані через admin
alert(user.name); // 'Петро', зміни видно в user
```
