# Типы данных

## Оглавление

- [Список типов](#TypesList)
- [Отображение типа](#Typeof)
- [Преобразование типов](#TypeConvertion)
  - [Преобразование к числу](#ConvertionToNumber)
  - [Преобразование к строке](#ConvertionToString)
  - [Преобразование к boolean](#ConvertionToBoolean)

## <a name="TypesList"></a> Список типов

- **number** - все числовые значения:
- **string** - любое символы и строки;
- **boolean** - true/false;
- **symbol** - специальный тип для создания объекта-обертки над любыми другими типами;
- **bigint** - тип, для обозначения специального объекта, позволяющего представить числа больше чем 23^53 - 1;
- **null** - тип, обозначающие отсутствие чего-либо (но является значением);
- **undefined** - тип, обозначающий отсутствие какого-либо значения;
- **function** - тип, обозначающий функцию;
- **object** - тип, обозначающий любые остальные структуры данных (Object, Map, Set, Array).

## <a name="Typeof"></a> Отображение типа

Для отображения типа используется унарный оператор [**typeof**](https://github.com/mikhaelzol93/JS-Reference/blob/main/doc/operators.md#Typeof):

```javascript
// Функции
function fd() {}
const fe = function () {};
const af = () => {};

// Классы
class Dog {}

// Вывод типов

console.log('Примитивные типы:\n');

console.log('Целое число:', typeof 1); // "number"
console.log('Дробное число:', typeof 2.5); // "number"
console.log('Infinity:', typeof Infinity); // "number"
console.log('NaN:', typeof NaN); // "number"
console.log('Большое число (BigInt):', typeof BigInt(1)); // "bigint"
console.log('Строка:', typeof 'str'); // "string"
console.log('Symbol:', typeof Symbol('str')); // "symbol"
console.log('Булевое значение:', typeof true); // "boolean"
console.log('null:', typeof null); // "object"
console.log('undefined:', typeof undefined); // "undefined"

console.log('\nФункции:\n');

console.log('Function Declaration:', typeof fd); // "function"
console.log('Function Expression:', typeof fe); // "function"
console.log('Arrow Function:', typeof af); // "function"

console.log('\nСтруктуры данных:\n');

console.log('Массив:', typeof []); // "object"
console.log('Объект:', typeof {}); // "object"
console.log('Map:', typeof new Map()); // "object"
console.log('Set:', typeof new Set()); // "object"

console.log('\nКлассы:\n');

console.log('Класс Dog:', typeof Dog); // "function"
```

## <a name="TypeConvertion"></a> Преобразование типов

### <a name="ConvertionToNumber"></a> Преобразование к числу

Для преобразования к числу используется унарный оператор [**+**](https://github.com/mikhaelzol93/JS-Reference/blob/main/doc/operators.md#ConvertionToNumber) или функция **Number(value)**:

```javascript
console.log('Положительное или отрицательное число:', +1); // 1
console.log('Ноль:', +0); // 1
console.log('NaN:', +NaN); // NaN
console.log('Infinity:', +Infinity); // Infinity
console.log('Строка:', +'1'); // 1
console.log('Пустая строка:', +''); // 1
console.log('True:', +true); // 1
console.log('False:', +false); // 0
console.log('Объект:', +{}); // NaN
console.log('Пустой массив:', +[]); // 0
console.log('Массив с данными:', +[1]); // 1
console.log('Map:', +new Map()); // NaN
console.log('Set:', +new Set([1])); // NaN
console.log('null:', +null); // 0
console.log('undefined:', +undefined); // NaN
```

**Важно:** преобразование _BigInt_ и _Symbol_ выдает ошибку.

Также, для консистентности и лучшей читаемости, рекомендуется всегда отдавать предпочтение **Number(value)** перед **+**.

### <a name="ConvertionToString"></a> Преобразование к строке

Преобразовать к строке можно с помощью функции **String(value)** или метода **.toString()**. Однако, так как метод .**.toString()** есть не у каждой сущности, надежнее и консистентнее всегда использовать **String(value)**.

Метод **.toString()** нельзя вызвать напрямую у литерала числа (например 1), null, undefined. Для этого необходимо их сначала записать в переменную, и только после этого вызвать у переменной метод **.toString()**.

```javascript
console.log('Число:', String(1)); // Значение числа в виде строки (1 => "1")
console.log('NaN:', NaN.toString()); // "NaN"
console.log('Infinity:', Infinity.toString()); // "Infinity"
console.log('BigInt(1):', BigInt(1).toString()); // Значение BigInt в виде строки (BigInt(1) => "1")
console.log('Строка:', '1'.toString()); // Строка так и останется строкой
console.log('Symbol:', Symbol('1').toString()); // Выведет "Symbol(value)" (Symbol(1) => "Symbol(1)")
console.log('Boolean:', true.toString()); // "true"
console.log('Объект:', {}.toString()); // "[object Object]"
console.log('Массив:', [1, 2, 3].toString()); // Выведет значение элементов массива через запятую ([1, 2].toString() => "1, 2")
console.log('Map:', new Map().toString()); // "[object Map]"
console.log('Set:', new Set().toString()); // "[object Set]"
console.log('null:', String(null)); // "null"
console.log('undefined:', String(undefined)); // "undefined"
```

### <a name="ConvertionToBoolean"></a> Преобразование к boolean

Для преобразования используется унарный оператор [**!!**](https://github.com/mikhaelzol93/JS-Reference/blob/main/doc/operators.md#ConvertionToBoolean) или функция **Boolean(value)**. Также, как в случае с числом и строкой предпочтительно использовать именно **Boolean(value)**.

```javascript
console.log('Положительное или отрицательное число:', !!1); // true
console.log('Ноль:', !!0); // false
console.log('NaN:', !!NaN); // false
console.log('Infinity:', !!Infinity); // true
console.log('BigInt:', !!BigInt(1)); // true
console.log('Строка:', !!'1'); // true
console.log('Пустая строка:', !!''); // false
console.log('Symbol:', !!Symbol('1')); // true
console.log('True:', !!true); // true
console.log('False:', !!false); // false
console.log('Объект:', !!{}); // true
console.log('Массив:', !![]); // true
console.log('Map:', !!new Map()); // true
console.log('Set:', !!new Set()); // true
console.log('null:', !!null); // false
console.log('undefined:', !!undefined); // false
```
