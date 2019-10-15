//-- Функция-стрелка -----------------------------------------------------------------
function square(x){
  return x*x;
}
или то же амое что
const sq = (x) => x*x;


//--Максимальное нечётное число
const arr = ['1', '3', '2', '4'];
const res = arr
  .map((el) => parseInt(el))
  .filter((num) => num%2)
  .reduce((max, value) => Math.max(max, value),0);
console.log(res);


//-- Значения аргументов по умолчанию -----------------------------------------------------------------
function fetchOrders(count = 10, start = 0)
{
  console.log('Getting', count, 'orders starting from', start);
}


//-- Rest-параметр, массив аргументов -----------------------------------------------------------------
function max(...numbers){
  console.log(numbers);
}


//-- Spread-оператор разворачивает массив на компоненты -----------------------------------------------------------------
const arr1 = [1, 2, 3];
const arr2 = [5, 6, 3];
const res = Math.max(...arr1, ...arr2);
console.log(res);

const shallowCopy = [...arr1, ...arr2, 8];		объединение массивов
console.log(shallowCopy);


//-- Destrucruring. позволяет достать значение из структуры данных -----------------------------------------------------------------
const person = {
  name:{
    first: 'Peter',
    last: 'Smith',  
  },
  age: 27
};
const {name:{first, last}} = person;
console.log(first, last);
const {role = 'user'} = person;		//значение по умолчанию

function connect({
  host = 'localhost',
  port = 8080,
  user = 'guest'} = {}){
  console.log('user:', user, 'port:', port, 'host:', host);
}
connect({port:1111});


//-- Деструктуризация массива -----------------------------------------------------------------
const fib = [1, 1, 2, 3, 5, 8, 13, 21];
const [a, b, c] = fib;
const [a, , b] = fib;
console.log(a, b, c);

const line = [[10, 17], [12, 5]];
const [[x1, y1], [x2, y2]] = line;
console.log(x1, y1, x2, y2);

const peoples = ['Chris', 'Sandra', 'Bob'];
const[p, ...others] = peoples;
console.log(others);

const dict = {
  duck: 'quack',
  dog: 'wuff',
  mouse: 'squeak',
  hamster: 'squeak'
};
//const res = Object.entries(dict) //переводит справочник в массив двумерный
//  .filter((arr) => arr[1]==='squeak');    //если пищит 
 const res = Object.entries(dict) //переводит справочник в массив двумерный
  .filter(([key, value]) => value==='squeak')    //если пищит 
  .map(([key]) => key);                         //только ключи
console.log(res);


//-- Шаблонные строки -----------------------------------------------------------------
const user = 'Andrey';
const num = 17;
const txt =`Hello ${user} you ${num} letters in your inbox.`;   //тут тильда, а не апостроф
const txt2 =`Hello ${user} you ${2+2} letters in your inbox.`;
const txt3 = `Сегодня ${Date.now()}`;
console.log(txt3);

const items = ['tea', 'coffee'];
const templateHtml = `
  <ul>
    <li>${items[0]}</li>
    <li>${items[1]}</li>
  </ul>
`;
console.log(templateHtml);


//-- Объекты -----------------------------------------------------------------
const x = 10;
const y = 30;
const point = {
  x,
  y,
  draw(ctx){
    //тело метода этого объекта
  }
}; 

const prefix = '_blah_';  //префикс
const data = {
  [prefix + 'name']: 'Bob',
  [prefix + 'age']: 23
};
console.log(data);

//копирование свойства объекта
const defaults = {
  host: 'localhost',
  dbName: 'blog',
  user: 'admin'
};
const opts = {
  user: 'john',
  password: 'utopia'
};
const res = Object.assign({}, defaults, opts);  //Object.assign(defaults, opts); - перезапишет defaults свойствами нового объекта
console.log(res);

const person = {
  name: 'Bob',
  friends: ['Mark', 'Jacob']
};
const shallowCopy = Object.assign({}, person);  //поверхностная копия объекта
person.friends.push('Jane');
console.log(shallowCopy);


//-- Objects Spread --------------------------------------------------
const defaults = {
  host: 'localhost',
  dbName: 'blog',
  user: 'admin'
};
const opts = {
  user: 'john',
  password: 'utopia'
};
const res = {...defaults, ...opts};   //копирование свойств через Spread
console.log(res);
или
const port = 8080;
const res = {   //копирование свойств через Spread
  ...defaults,
  ...opts,
  port,
  connect(){
    //какой-то метод
  }
};
console.log(res);



//-- Прототипы ----------------------------------------------------------------
1. Через setPrototypeOf(ТАК ЛУЧШЕ НЕ ДЕЛАТЬ. МЕДЛЕННО):
const animal = {
  say: function(){
    console.log(this.name, 'goes', this.voice);
  }
};
const dog = {
  name: 'dog',
  voice: 'woof',
};
Object.setPrototypeOf(dog, animal); //ТАК ЛУЧШЕ НЕ ДЕЛАТЬ. МЕДЛЕННО
const cat = {
  name: 'cat',
  voice: 'meow',
};
Object.setPrototypeOf(cat, animal);
dog.say();
cat.say();

2. Через создание объекта(как конструктор):
function Animal(name, voice){
  this.name = name;
  this.voice = voice;
}
Animal.prototype.say = function(){
  console.log(this.name, 'goes', this.voice);
};
const dog = new Animal('Dog', 'woof');
const cat = new Animal('Cat', 'meow');
dog.say();
cat.say();


//-- Классы ----------------------------------------------
class Animal{
  constructor(name, voice){
    this.name = name;
    this.voice = voice;
  }
  say(){
    console.log(this.name, 'goes', this.voice);
  }
}
class Bird extends Animal{
  constructor(name, voice, canFly){
    super(name, voice);
    this.canFly = canFly;
  }
  say(){
    super.say();  //так можно вызвать метод из суперкласса
    console.log('Birds don\'t like to talk');
  }
}
const duck = new Bird('Duck', 'quack', true);
duck.say();


//-- Class properties --------------------------------
class Counter {
  count = 1;

  inc = () =>{
    this.count += Counter.incStep;
    console.log(this.count);
  }
  static incStep = 2;
  static incrementAll = function(arr){
    arr.forEach((c) => c.inc());
  };
}
Counter.incrementAll([]);
const cnt = new Counter();
console.log(cnt.count);
cnt.inc();
setTimeout(cnt.inc, 1000);



//-- Модули в JavaScript --------------------------------
в модуле:
export{
  add, subtract, multiply, divide, PI   //именованый экспорт, где перечисляются функции модуля
}
export default Graph; //экспорт по умолчанию

там куда экспортируем:
//import {add, subtract, PI} from './mymath';
//console.log(add(2, 2), PI);

//import * as calc from './mymath';
//console.log(calc.PI)

//import Graph from './mymath';
//console.log(typeof Graph);

//import G1, {add, subtract} from './mymath';
//console.log(typeof G1);

import G1, * as calc from './mymath';
console.log(typeof G1);

Вообще при объявлении класса в модуле можно сразу указать
export default class Graph { и т.д.

//вставка кода из модуля
import './sideeffect';

//импорт модуля подключенного
import joker from 'one-liner-joke';



























