# Формат JSON, метод toJSON
JSON, який використовується для представлення об'єктів у вигляді рядка.

Це один з найбільш зручних форматів даних при взаємодії з JavaScript. Якщо потрібно з сервера взяти об'єкт з даними і передати на клієнті, то в якості проміжного формату - для передачі по мережі, майже завжди використовують саме його..
```
var user = '{ "name": "Вася", "age": 35, "isAdmin": false, "friends": [0,1,2,3] }';

user = JSON.parse(user);

alert( user.friends[1] ); // 1
```
##JSON-об'єкти ≠ JavaScript-об'єкти
```
{
  name: "Вася",       // ошибка: ключ name без кавычек!
  "surname": 'Петров',// ошибка: одинарные кавычки у значения 'Петров'!
  "age": 35,           // .. а тут всё в порядке.
  "isAdmin": false    // и тут тоже всё ок
}
```

## Cеріалізация, метод JSON.stringify
```
var event = {
  title: "Конференція",
  date: "сьогодні"
};

var str = JSON.stringify(event);
alert( str ); // {"title":"Конференція","date":"сьогодні"}

// Зворотне перетворення.
event = JSON.parse(str);
```

##методи об'єктів, this

```
var user = {
  name: 'Василь',

  // метод
  sayHi: function() {
    alert( 'Привіт!' );
  }

};

user.sayHi();
```
```
var user = {
  name: 'Василь'
};

user.sayHi = function() { // присвоїли метод після створення об'єкта
  alert('Привет!');
};

// Виклик:
user.sayHi();
```
#Доступ до об'єкту через this
```
var user = {
  name: 'Василь',

  sayHi: function() {
    alert( this.name );
  }
};

user.sayHi(); // sayHi в контексте user
```
Замість this всередині sayHi можна було б звернутися до об'єкта, використовуючи змінну user:
```
 sayHi: function() {
    alert( user.name );
  }
```
Однак, таке рішення нестабільно. Якщо ми вирішимо скопіювати об'єкт в іншу змінну, наприклад admin = user
```
var user = {
  name: 'Василь',

  sayHi: function() {
    alert( user.name ); // буде помилка
  }
};

var admin = user;
user = null;

admin.sayHi(); 
```
Через this метод може не тільки звернутися до будь-якого властивості об'єкта, а й передати кудись посилання на сам об'єкт цілком:
```
var user = {
  name: 'Василь',

  sayHi: function() {
    showName(this); // передати поточний об'єкт в showTime
  }
};

function showName(namedObj) {
  alert( namedObj.name );
}

user.sayHi(); // Василь
```
Будь-яка функція може мати в собі this. Абсолютно неважливо, оголошена чи вона в об'єкті або окремо від нього.
```
var user = { firstName: "Вася" };
var admin = { firstName: "Адмін" };

function func() {
  alert( this.firstName );
}

user.f = func;
admin.g = func;

// this равен объекту перед точкой:
user.f(); // Вася
admin.g(); // Адмін
admin['g'](); // Адмін (не важливо, доступ до об'єкту через точку або квадратні дужки)
```
Значення this при виклику без контексту
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
#Створення об'єктів через "new"
Звичайний синтаксис {...} дозволяє створити один об'єкт. Але найчастіше потрібно створити багато однотипних об'єктів.

Для цього використовують «функції-конструктори», запускаючи їх за допомогою спеціального оператора new.
##Конструктор
Конструктором стає будь-яка функція, викликана через new.
```
function Animal(name) {
  this.name = name;
  this.canWalk = true;
}

var animal = new Animal("їжачок");
```
технічно, будь-яка функція може бути використана як конструктор,
Але, щоб виділити функції, задумані як конструктори, їх називають з великої літери: Animal, а не animal.
В результаті виклику new Animal ("їжачок"); отримуємо такий об'єкт:
```
animal = {
  name: "їжачок",
  canWalk: true
}
```
Іншими словами, при виклику new Animal відбувається щось в такe
```
function Animal(name) {
  // this = {};

  // в this пишемо властивості, методи
  this.name = name;
  this.canWalk = true;

  // return this;
}
```
##Правила обробки return
- Коли Ви викликаєте return з об'єктом, буде повернуто він, а не this.
- Коли Ви викликаєте return з примітивним значенням, воно буде відкинуте.
```
function BigAnimal() {

  this.name = "Мышь";

  return { name: "Годзилла" };  // <-- поверне об'єкт
}

alert( new BigAnimal().name );  // Годзилла, отримали об'єкт замість this
```
```
function BigAnimal() {

  this.name = "Мышь";

  return "Годзилла"; // <-- вернем примітив
}

alert( new BigAnimal().name ); // Миша, отримали this (а Годзилла зник)
```
##Створення методів в конструкторі
```
function User(name) {
  this.name = name;

  this.sayHi = function() {
    alert( "Моє ім'я: " + this.name );
  };
}

var ivan = new User("Іван");

ivan.sayHi(); // Моє ім'я: Іван

```
##локальні змінні
```
function User(firstName, lastName) {
  // допоміжна змінна
  var phrase = "Привіт";

  //  допоміжна вкладена функція
  function getFullName() {
      return firstName + " " + lastName;
    }

  this.sayHi = function() {
    alert( phrase + ", " + getFullName() ); 
  };
}

var vasya = new User("Вася", "Петрович");
vasya.sayHi(); // Привіт, Вася Петрович
```
