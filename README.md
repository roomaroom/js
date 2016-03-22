# Формат JSON, метод toJSON
JSON, который используется для представления объектов в виде строки.

Это один из наиболее удобных форматов данных при взаимодействии с JavaScript. Если нужно с сервера взять объект с данными и передать на клиенте, то в качестве промежуточного формата – для передачи по сети, почти всегда используют именно его.
```
var user = '{ "name": "Вася", "age": 35, "isAdmin": false, "friends": [0,1,2,3] }';

user = JSON.parse(user);

alert( user.friends[1] ); // 1
```
##JSON-объекты ≠ JavaScript-объекты
```
{
  name: "Вася",       // ошибка: ключ name без кавычек!
  "surname": 'Петров',// ошибка: одинарные кавычки у значения 'Петров'!
  "age": 35,           // .. а тут всё в порядке.
  "isAdmin": false    // и тут тоже всё ок
}
```

## Сериализация, метод JSON.stringify
```
var event = {
  title: "Конференция",
  date: "сегодня"
};

var str = JSON.stringify(event);
alert( str ); // {"title":"Конференция","date":"сегодня"}

// Обратное преобразование.
event = JSON.parse(str);
```

#Методы объектов, this

##Методы у объектов
```
var user = {
  name: 'Василий',

  // метод
  sayHi: function() {
    alert( 'Привет!' );
  }

};

// Вызов
user.sayHi();
```
```
var user = {
  name: 'Василий'
};

user.sayHi = function() { // присвоили метод после создания объекта
  alert('Привет!');
};

// Вызов метода:
user.sayHi();
```
#Доступ к объекту через this
```
var user = {
  name: 'Василий',

  sayHi: function() {
    alert( this.name );
  }
};

user.sayHi(); // sayHi в контексте user
```
Вместо this внутри sayHi можно было бы обратиться к объекту, используя переменную user:
```
 sayHi: function() {
    alert( user.name );
  }
```
Однако, такое решение нестабильно. Если мы решим скопировать объект в другую переменную, например admin = user
```
var user = {
  name: 'Василий',

  sayHi: function() {
    alert( user.name ); // приведёт к ошибке
  }
};

var admin = user;
user = null;

admin.sayHi(); 
```
Через this метод может не только обратиться к любому свойству объекта, но и передать куда-то ссылку на сам объект целиком:
```
var user = {
  name: 'Василий',

  sayHi: function() {
    showName(this); // передать текущий объект в showName
  }
};

function showName(namedObj) {
  alert( namedObj.name );
}

user.sayHi(); // Василий
```
Любая функция может иметь в себе this. Совершенно неважно, объявлена ли она в объекте или отдельно от него.
```
ar user = { firstName: "Вася" };
var admin = { firstName: "Админ" };

function func() {
  alert( this.firstName );
}

user.f = func;
admin.g = func;

// this равен объекту перед точкой:
user.f(); // Вася
admin.g(); // Админ
admin['g'](); // Админ (не важно, доступ к объекту через точку или квадратные скобки)
```
Значение this при вызове без контекста
```
function func() {
  alert( this ); // выведет [object Window] или [object global]
}

func();

function func() {
  "use strict";
  alert( this ); // выведет undefined (кроме IE9-)
}

func();

```
