---
title: Оператор Запятая
slug: Web/JavaScript/Reference/Operators/Comma_operator
---

{{jsSidebar("Operators")}}

**Оператор запятая** выполняет каждый из его операндов (слева направо) и возвращает значение последнего операнда.

{{InteractiveExample("JavaScript Demo: Expressions - Comma operator")}}

```js interactive-example
let x = 1;

x = (x++, x);

console.log(x);
// Expected output: 2

x = (2, 3);

console.log(x);
// Expected output: 3
```

## Синтаксис

```
expr1, expr2, expr3...
```

## Параметры

- `expr1`, `expr2, expr3...`
  - : Любые выражения.

## Описание

Вы можете использовать оператор запятая, когда необходимо включить несколько выражений в место, которое принимает только одно выражение. Наиболее частый пример использования этого оператора - это передача нескольких параметров в цикл `for`.

## Примеры

Если `a` это двумерный массив элементов размерностью 10 х 10, то приведённый ниже код использует оператор запятая для одновременного изменения двух переменных за раз.

Следующий код выводит в консоль значения диагональных элементов массива:

```js
for (let i = 0, j = 9; i <= 9; i++, j--)
  console.log("a[" + i + "][" + j + "] = " + a[i][j]);
```

Заметьте, что запятая при объявлении переменной `var`, `let` или `const` **не** является оператором запятая, так как в данном случае она находится не в выражении. Скорее, это спец символ в объявлении переменных, комбинирующий их множество в одно выражение. Практически, эта запятая ведёт себя почти так же, как и запятая.

```js
// подобное объявление запрещено в строгом режиме(strict mode)

((a = b = 3), (c = 4)); // возвращает 4 в консоль
console.log(a); // 3
x = ((y = 5), (z = 6)); // возвращает 6 в консоль
console.log(x); // 6
```

Оператор запятая полностью отличается от запятой в массивах, объектах, аргументах и параметрах функции.

### Вычисления и возврат значения

Другой пример использования оператора запятой – вычисления перед возвратом значения. Как было указано ранее, будет возвращён только последний элемент, но все предыдущие также будут вычислены. Таким образом можно сделать:

```js
function myFunc() {
  let x = 0;

  return ((x += 1), x); // то же самое, что return ++x;
}
```

## Спецификации

{{Specifications}}

## Совместимость с браузерами

{{Compat}}

## Смотрите также

- [for loop](/ru/docs/Web/JavaScript/Reference/Statements/for)
