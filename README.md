# ReactSamples
React samples for study

//-- Функция-стрелка
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


//-- Значения аргументов по умолчанию
function fetchOrders(count = 10, start = 0)
{
  console.log('Getting', count, 'orders starting from', start);
}


//-- Rest-параметр, массив аргументов
function max(...numbers){
  console.log(numbers);
}


//-- Spread-оператор разворачивает массив на компоненты
const arr1 = [1, 2, 3];
const arr2 = [5, 6, 3];
const res = Math.max(...arr1, ...arr2);
console.log(res);

const shallowCopy = [...arr1, ...arr2, 8];		объединение массивов
console.log(shallowCopy);


//-- Destrucruring. позволяет достать значение из структуры данных
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

//-- Деструктуризация массива
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
