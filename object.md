#cоздание объектов
```
o = new Object();
o = {}; // пустые фигурные скобки
```
Объект может содержать в себе любые значения, которые называются свойствами объекта
```
var person = {};
person.name = 'Вася';

person.age = 25;
alert( person.name + ': ' + person.age );

var person = {
  name: "Василий",
  age: 25
};

```
```
delete person.age;
```
Иногда бывает нужно проверить, есть ли в объекте свойство с определенным ключом.

Для этого есть особый оператор: "in".
```
if ("name" in person) {
  alert( "Свойство name существует!" );
}
alert( person.lalala === undefined );
```
##доступ через квадратные скобки
```
var person = {};
person['name'] = 'Вася'; // то же что и person.name = 'Вася'
```
##Доступ к свойству через переменную
```
var person = {};
person.age = 25;
var key = 'age';

alert( person[key] ); // выведет person['age']
```
##Названия свойств можно перечислять как в кавычках, так и без
```
var menuSetup = {
  width: 300,
  'height': 200,
  "мама мыла раму": true
};
```
##В качестве значения можно тут же указать и другой объект:
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

##Объекты: перебор свойств
##for..in
```
for (key in obj) {
  /* ... делать что-то с obj[key] ... */
}
var menu = {
  width: 300,
  height: 200,
  title: "Menu"
};

for (var key in menu) {
  // этот код будет вызван для каждого свойства объекта
  // ..и выведет имя свойства и его значение

  alert( "Ключ: " + key + " значение: " + menu[key] );
}
```
