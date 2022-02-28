# Операторы в JavaScript

## Оглавление

- [Общая информация](#General)
- [Унарные операторы](#Unary)
  - [Удаление свойства объекта или элемента массива (delete)](#Delete)
  - [Проверка типа элемента (typeof)](#Typeof)
  - [Преобразование к числу (+)](#ConvertionToNumber)
  - [Преобразование к boolean (!!)](#ConvertionToBoolean)
  - [Отрицание (!)](#Negation)
  - [Операторы инкремента и декремента (++, --)](#IncrementAndDecrement)
- [Бинарные операторы](#Binary)
  - [Операторы сравнения](#Comparison)
  - [Строго равно по типу и по значению (===)](#StrictEquality)
  - [Строго не равно по типу или по значению (!==)](#StrictNonEquality)
  - [Строго меньше/больше и меньше или равно/больше или равно (<, >, <=, >=)](#GreaterOrLessComprasion)
  - [Логический оператор "ИЛИ" (||)](#LogicalOr)
  - [Логический оператор "И" (&&)](#LogicalAnd)
  - [Арифметические операторы (+, -, \*, /, \*\*, %)](#ArithmeticOperators)
  - [Операторы присваивания (=, +=, -=, \=, \*=, %=)](#AssignmentOperators)
  - [Проверка на инстанс объекта (instanceof)](#Instanceof)
  - [Проверка на свойство объекта (in)](#PropertyIn)
- [Тернарные операторы](#TernaryOperators)
  - [Условный оператор (? :)](#ConditionalOperator)

## <a name="General"></a> Общая информация

- **Операнд** - это выражение (expression) или утверждение (statement), с которым работает оператор;
- **Оператор** - это встроенный в JavaScript обработчик операндов.

Пример операторов и операндов:

```javascript
const x = 5; // "x", "5" - операнды, "=" - оператор присваивания
console.log(5 > 6); // "5", "6" - операнды, ">" - оператор сравнения
console.log(typeof x); // "x" - операнд, "typeof" - оператор проверки типа
```

## <a name="Unary"></a> Унарные операторы

Операторы, которые работают только с одним операндом.

### <a name="Delete"></a> Удаление свойства объекта или элемента массива (delete)

Данный оператора работает только с **собственными** свойствами объекта.

```javascript
const obj = {
  x: 1,
  y: 2,
};

const arr = [1, 2];

delete obj.y;
console.dir(obj); // { x: 1 }

delete arr[1];
console.log(arr); // [1, undefined]
```

### <a name="Typeof"></a> Проверка типа элемента (typeof)

Унарный оператор **typeof** возвращает строковое значение типа сущности.

Возможные варианты вывода:

- **number**;
- **string**;
- **boolean**;
- **object**;
- **symbol**;
- **bigint**;
- **function**.
- **undefined**.

По историческим причинам, тип **null** - это _object_.
Также, если создать класс и вывести его тип, то мы получим **function**.

```javascript
console.log('typeof числа:', typeof 1); // number
console.log('typeof объекта:', typeof {}); // object
console.log('typeof массива:', typeof []); // object
console.log('typeof null:', typeof null); // object
```

Подробнее о типах можно почитать в [этой](https://github.com/mikhaelzol93/JS-Reference/blob/main/doc/types.md) статье.

### <a name="ConvertionToNumber"></a> Преобразование к числу (+)

Преобразовывает сущность к числовому типу. Если преобразование невозможно вернет _NaN_.

Также, если попытаться преобразовать _BigInt_ и _Symbol_, то получим ошибку.

Примеры преобразований: [здесь](https://github.com/mikhaelzol93/JS-Reference/blob/main/doc/types.md#ConvertionToNumber).

### <a name="ConvertionToBoolean"></a> Преобразование к boolean (!!)

Преобразовывает сущность к булевому типу.

Примеры преобразований: [здесь](https://github.com/mikhaelzol93/JS-Reference/blob/main/doc/types.md#ConvertionToBoolean).

### <a name="Negation"></a> Отрицание (!)

Работает так же, как и приведение к булевому значению, но меняет значение на противоположное
(там, где **!!** вернет _true_, **!** вернет _false_ и наоборот).

```javascript
console.log('Положительное или отрицательное число:', !1); // false
console.log('Ноль:', !0); // true
console.log('NaN:', !NaN); // true
console.log('Infinity:', !Infinity); // false
console.log('BigInt:', !BigInt(1)); // false
console.log('Строка:', !'1'); // false
console.log('Пустая строка:', !''); // true
console.log('Symbol:', !Symbol('1')); // false
console.log('True:', !true); // false
console.log('False:', !false); // true
console.log('Объект:', !{}); // false
console.log('Массив:', ![]); // false
console.log('Map:', !new Map()); // false
console.log('Set:', !new Set()); // false
console.log('null:', !null); // true
console.log('undefined:', !undefined); // true
```

### <a name="IncrementAndDecrement"></a> Операторы инкремента и декремента (++, --)

Данные операторы увеличивают или уменьшают число на 1.

```javascript
let x = 1;
x++;
console.log(x); // 2
```

Данный оператор можно ставить как перед переменной, так и после неё:

```javascript
let x = 1;
x++; // постинкремент
++x; // преинкремент
x--; // постдекремент
--x; // предекремент
```

Между работой преинкремента/декремента и постинкремента/декремента есть разница. Все дело в том, что эти операторы меняют значение переменной, а также возвращают результат. Однако, возвращаемый результат разный:

- Преинкремент/декремент - изменяет значение переменной и возвращает **обновленное** значение;
- Постинкремент/декремент - изменяет значение переменной и возвращает **изначальное** значение.

Вот так работает на примере преинкремент:

```javascript
let x = 1;
const y = ++x;
console.log(x); // 2 - увеличил значение на 1
console.log(y); // 2 - вернул обновленное значение
```

А вот так постинкремент:

```javascript
let x = 1;
const y = x++;
console.log(x); // 2 - увеличил значение на 1
console.log(y); // 1 - вернул изначальное значение
```

Как видно из этих примеров, значение _x_ в обоих случаях изменяется одинаково, различаются лишь возвращаемые значения (которые мы записываем в _y_). Поэтому, если нам нужно изменить изначальное значение переменной, то нет разницы, что использовать. А вот если нам нужно работать с _y_, то есть с измененным значением, то чаще всего необходимо использовать преинкремент/декремент.

Также, так как постинкремент/декремент возвращает изначальное значение, он расходует больше оперативной памяти в своей работе. Отсюда вывод, что лучше всегда использовать преинкремент/декремент, так как чаще всего нам нужно именно такое поведение (что минимизирует вероятность ошибок) и хоть незначительно, но оптимальнее по ресурсам. А постинкремент/декремент нужно использовать только если после изменения переменной нам нужно работать с изначальным значением.

**Важно:** изначальная переменная (в нашем случае _x_) должна быть именно переменной. Если сделать её константой - мы получим ошибку.

Также, если _x_ будет не числового типа, то вначале произойдет преобразование к числу, а потом уже сама операция. Подробнее о преобразованиях к числу [здесь](https://github.com/mikhaelzol93/JS-Reference/blob/main/doc/types.md#ConvertionToNumber). Соответственно, мы можем получить _NaN_ или ошибку в результате преобразования.

## <a name="Binary"></a> Бинарные операторы

Операторы, которые работают с двумя операндами.

### <a name="Comparison"></a> Операторы сравнения

Сравнивают два операнда и возвращают _true_ или _false_.

### <a name="StrictEquality"></a> Строго равно по типу и по значению (===)

```javascript
console.log('Целые числа:', 1 === 1); // true
console.log('Дробные числа:', 1.2 === 1.2); // true
console.log('NaN:', NaN === NaN); // false
console.log('Infinity:', Infinity === Infinity); // true
console.log('BigInt:', BigInt(1) === BigInt(1)); // true
console.log('Строка:', '1' === '1'); // true
console.log('Пустая строка:', '' === ''); // true
console.log('Symbol:', Symbol('1') === Symbol('1')); // false
console.log('True:', true === true); // true
console.log('False:', false === false); // true
console.log('Объект:', {} === {}); // false
console.log('Массив:', [] === []); // false
console.log('Map:', new Map() === new Map()); // false
console.log('Set:', new Set() === new Set()); // false
console.log('null:', null === null); // true
console.log('undefined:', undefined === undefined); // true
```

### <a name="StrictNonEquality"></a> Строго не равно по типу или по значению (!==)

По-факту, противоположный результат, чем тот, что возвращает строго равно.

```javascript
console.log('Целые числа:', 1 !== 1); // false
console.log('Дробные числа:', 1.2 !== 1.2); // false
console.log('NaN:', NaN !== NaN); // true
console.log('Infinity:', Infinity !== Infinity); // false
console.log('BigInt:', BigInt(1) !== BigInt(1)); // false
console.log('Строка:', '1' !== '1'); // false
console.log('Пустая строка:', '' !== ''); // false
console.log('Symbol:', Symbol('1') !== Symbol('1')); // true
console.log('True:', true !== true); // false
console.log('False:', false !== false); // false
console.log('Объект:', {} !== {}); // true
console.log('Массив:', [] !== []); // true
console.log('Map:', new Map() !== new Map()); // true
console.log('Set:', new Set() !== new Set()); // true
console.log('null:', null !== null); // false
console.log('undefined:', undefined !== undefined); // false
```

### <a name="GreaterOrLessComprasion"></a> Строго меньше/больше и меньше или равно/больше или равно (<, >, <=, >=)

Сравнивают операнды на то, кто из них больше (или равен) и возвращают _true_ или _false_.

**Важно:** если операнд представлен не числовым типом, то вначале произойдет приведение его к числу, и только после этого произойдет сравнение. Отсюда следуют несколько правил:

- Любое число + операнд, который приводится к NaN, всегда будут давать _false_;
- Если оба операнда приводятся к _NaN_ и представляют собой один тип (например object или map), то их строгое сравнение даст _false_, а не строгое - _true_;
- Если оба операнда приводятся к _NaN_ и представляют собой разные типы (например object и map), то любое их сравнение даст _false_;
- Так как пустой массив приводится к 0, а с значениями - к 1, то пустой массив всегда строго меньше наполненного;
- null приводится к нулю, следовательно он меньше 1, но больше -1;
- -Infinity всегда строго меньше нуля и любого отрицательного числа, а Infinity всегда строго больше нуля и любого числа в принципе.

### <a name="LogicalOr"></a> Логический оператор "ИЛИ" (||)

Возвращает _true_ если хотя бы один из операндов приводится к _true_.

```javascript
console.log(2 > 5 || 2 < 5); // true
console.log(2 > 5 || 2 < 1); // false
```

### <a name="LogicalAnd"></a> Логический оператор "И" (&&)

Возвращает _true_ если оба из операндов приводятся к _true_.

```javascript
console.log(2 < 5 && 2 > 1); // true
console.log(2 > 5 && 2 < 5); // false
```

### <a name="ArithmeticOperators"></a> Арифметические операторы (+, -, \*, /, \*\*, %)

Данные операторы производят арифметические действия с числами (и в случае с _+_ - с строками).

Перед проведением арифметических операций происходит преобразование операндов к числам. Подробнее про это [здесь](https://github.com/mikhaelzol93/JS-Reference/blob/main/doc/types.md#ConvertionToNumber).

```javascript
console.log('Сложение двух чисел:', 1 + 6); // 7
console.log('Сложение двух строк:', 'Hello ', 'World'); // "Hello World"
console.log('Вычитание двух чисел:', 6 - 3); // 3
console.log('Умножение двух чисел:', 2 * 3); // 6
console.log('Деление двух чисел:', 6 / 3); // 2
console.log('Возведение числа в степень:', 2 ** 3); // 8
console.log('Остаток от деления (делится нацело):', 6 % 3); // 0
console.log('Остаток от деления (делится с остатком):', 7 % 3); // 1
```

### <a name="AssignmentOperators"></a> Операторы присваивания (=, +=, -=, \=, \*=, %=)

Операторы присваивания - присваивают идентификатору (переменной или константе) конкретное значение.

В случае с оператором **=** - происходит простое присвоение значения, тогда как в случае остальных операторов присваивания, происходит вычисление арифемитической операции.

Также, как и с арифметическими операциями, вначале происходит преобразование операндов к числам если это требуется.

```javascript
const x = 5; // Присвоили константе x значение 5
const y = x; // Присвоили константе y значение x

console.log(x); // 5
console.log(y); // 5

let num = 4;
console.log(num); // 4

num += 2; // 6, так как 4 + 2 = 6
num -= 2; // 4, так как 6 - 2 = 4
num /= 2; // 2, так как 4 / 2 = 2
num *= 3; // 6, так как 2 * 3 = 6
num %= 3; // 0, так как 6 делится без остатка на 3
```

### <a name="Instanceof"></a> Проверка на инстанс объекта (instanceof)

Все JavaScript объектноподобные сущности являются инстансами каких-либо объектов (глобальных или локальных). Оператор **instanceof** возвращает информацию о том, инстансом чего является та или иная сущность.

```javascript
class Dog {}
const dog = new Dog();

function fd() {}
const fe = function () {};
const af = () => {};

console.log('\nФункции:\n');

console.log('Function Declaration', fd instanceof Function); // true
console.log('Function Expression', fe instanceof Function); // true
console.log('Arrow Function', af instanceof Function); // true

console.log('\nСтруктуры данных:\n');

console.log('Инстанс класса Dog:', dog instanceof Dog); // true
console.log('Литерал объекта:', {} instanceof Object); // true
console.log('Map:', new Map() instanceof Map); // true
console.log('Set:', new Set() instanceof Set); // true
console.log('Массив:', [] instanceof Array); // true
```

**Важно:** любой из описанных примеров выше является инстансом _Object_, поэтому данная проверка является не безопасной (так как вы можете ожидать, например, объект, а вам придет массив или ссылка на функцию). Поэтому, целесообразнее использовать этот оператор не для объектов, а для остальных структур (массивов, функций и так далее). Или же, проверять инстанс конкретного известного вам объекта (как с инстансом класса _Dog_ из примера выше).

```javascript
class Dog {}
const dog = new Dog();

function fd() {}
const fe = function () {};
const af = () => {};

console.log('\nФункции:\n');

console.log('Function Declaration', fd instanceof Object); // true
console.log('Function Expression', fe instanceof Object); // true
console.log('Arrow Function', af instanceof Object); // true

console.log('\nСтруктуры данных:\n');

console.log('Инстанс класса Dog:', dog instanceof Object); // true
console.log('Литерал объекта:', {} instanceof Object); // true
console.log('Map:', new Map() instanceof Object); // true
console.log('Set:', new Set() instanceof Object); // true
console.log('Массив:', [] instanceof Object); // true
```

При этом, все примитивные типы дают _false_ при использовании _instanceof_, причем что при работе со своими глобальными объектами, что при проверке на инстанциирование от _Object_.

```javascript
console.log('\nПроверка примитивов на инстанс от глобальных объектов:\n');

console.log('Число от Number:', 1 instanceof Number); // false
console.log('Строка от String:', 'Hello' instanceof String); // false
console.log('Boolean от Boolean:', true instanceof Boolean); // false
console.log('Symbol от Symbol:', Symbol() instanceof Symbol); // false
console.log('BigInt от BigInt:', BigInt(1) instanceof BigInt); // false

console.log('\nПроверка примитивов на инстанс от Object:\n');

console.log('Число от Object:', 1 instanceof Object); // false
console.log('Строка от Object:', 'Hello' instanceof Object); // false
console.log('Boolean от Object:', true instanceof Object); // false
console.log('Symbol от Object:', Symbol() instanceof Object); // false
console.log('BigInt от Object:', BigInt(1) instanceof Object); // false
console.log('undefined от Object:', undefined instanceof Object); // false
console.log('null от Object:', null instanceof Object); // false
```

## <a name="PropertyIn"></a> Проверка на свойство объекта (in)

Оператор **in** проверяет, что объект имеет то или иное свойство:

```javascript
const user = {
  name: 'Вася',
};

console.log('Свойство существует в объекте:', 'name' in user); // true
console.log('Свойство не существует в объекте:', 'age' in user); // false
```

Данный оператор работает и с массивами, однако проверять нужно наличие индекса:

```javascript
const fruits = ['Apple', 'Orange'];

console.log('Обращение по значению элемента массива:', 'Apple' in fruits); // false
console.log('Проверка индекса в массиве:', '0' in fruits); // true
console.log('Проверка несуществующего индекса в массиве:', '3' in fruits); // false, так как последний индекс в массиве - 1
```

Нужно помнить, что оператор **in** учитывает все свойства объекта, в том числе и которые он наследует. Например, все объекты в JavaScript имеют метод (в случае с оператором **in** он не разделяет свойства и методы) _toString()_, поэтому вывод проверки этого свойства будет такой:

```javascript
console.log('Проверка на наследуемое свойство:', 'toString' in {}); // true
```

Точно так же это работает и с классами:

```javascript
class Animal {
  constructor() {
    this.type = 'Animal';
  }
}

class Dog extends Animal {
  constructor() {
    super();
    this.age = 2;
  }
}

console.log('Собственное свойство инстанса', 'age' in new Dog()); // true
console.log('Свойство глобального объекта Object', 'type' in new Dog()); // true
```

## <a name="TernaryOperators"></a> Тернарные операторы

Тернарные операторы работают с тремя операндами

### <a name="ConditionalOperator"></a> Условный оператор (? :)

Производит проверку какого-либо условия, которое указывается до _?_, если условие истино - выполняется то выражение, которое стоит после _?_, если ложно, то выполняется выражение, которое стоит после _:_

```javascript
const x = 5;

x < 4 ? console.log('Меньше') : console.log('Больше'); // "Больше"
```
