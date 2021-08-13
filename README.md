# Домашнее задание к лекции 2. «Функции»

## Задача № 1

Требуется написать функцию `getArrayParams(arr)`, которая получает на вход массив чисел от -100 до 100 и возвращает минимальное, максимальное и среднее арифметическое значений массива. 

1. Создайте функцию которая принимает на вод массив. 
2. Внутри функции задайте 3 переменных `min, max, sum` присвоив им некоторые первоначальные значения.
<details>
  <summary>Какие значения? (внутри подсказка, подумайте прежде чем открыть)</summary>
    min =  Infinity
    max = -Infinity
        
    Также можно использовать в качестве min и max первый элемент массива.
</details>

3. Пройдите по массиву циклом `for` либо `while` и для каждого элемента определите:
    1. Если элемент больше предыдущего максимума, то максимум становится равен элементу
    2. Если элемент меньше предыдущего минимума, то минимум становится равен элементу
    3. Добавляем элемент к сумме `sum` для последующего вычисления среднего.
4. После прохождения цикла функция должна возвращать объект вида: `{max:..., min: ..., avg:...}`, то есть минимальное, максимальное и средние значения. Чтобы вычислить среднее надо сумму элементов поделить на их количество. Среднее надо округлить до 2х знаков после запятой (для округления воспользуйтесь `toFixed`). Заметьте, `toFixed` возвращает `string`, так как вам необходимо вернуть число (`number`), то необходимо дополнительное преобразование значения к числу.

### Пример
```js
getArrayParams([-99, 99, 10]) // { min: -99, max: 99, avg: `3.33` }
getArrayParams([1, 2, 3, -100, 10])  // { min: -100, max: 10, avg: `-16.80` }
```

## Задача № 2
Представьте, что у нас есть мясорубка с разными насадками. Мясорубка запускает процесс, а сам процесс зависит от того, какая будет насадка.  Затем мясорубка применяет насадку ко всему мясу, которое в неё поступает и выдаёт на выход только самый лучший кусок.

Пусть дан массив, каждый элемент которого в свою очередь является массивом чисел, например `arrOfArr=[[1, 2, 3, 4], [10, 20, -10, -20]]`. Необходимо среди всех массивов найти такой, сумма элементов которого максимальна и вывести сумму.

Задачу можно разбить на две части:

- написать функцию, которая будет считать сумму элементов массива - это "насадка мясорубки"
- написать функцию, которая применит "насадку" ко всем массивам, которые поступили нам на вход  - это "мясорубка"
- тогда входные данные, массив массивов, являются "мясом"

Итак, напишем две функции: `mincer(arrOfArr,func)` - в наших терминах это мясорубка и `worker(arr)` - это насадка.

1. Напишите функцию `worker` которая должна находить сумму элементов массива и возвращать её. 

2. Функция `mincer`  принимает входные данные - массив массивов (мясо) и функцию `worker` - это насадка, таким образом `mincer` - функция высшего порядка. 

3. Затем `mincer` применяет полученную функцию `worker` к каждому из полученных массивов `worker(arrOfArr[i])` вычисляя таким образом сумму элементов. 

4. Если сумма больше предыдущего максимума, то меняем максимум (его следует хранить в отдельной переменной и задавать в начале функции `mincer`)

Таким образом наша мясорубка не только перемалывает (находит сумму чисел каждого массива) но и возвращает самый жирный кусок (с максимальной суммой) 

**Совет**: Напишите функцию `worker`, которая должна находить максимальное значение элементов массива и возвращать её.
Протестируйте функцию отдельно на своих примерах, например на (https://jsbin.com). Убедитесь, что она работает.
Затем передайте её в `mincer` (обратите внимание, что внутри она попадет в переменную `func` и мы сможем вызывать её `func(arr)`).
Итерируйтесь по массиву `arrOfArr` с помощью цикла, выполняя `worker` для каждого элемента (находя сумму), и если она больше ранее найденного максимума - присваивайте `max = sum`.

## Задача 3. 
Попробуем реализовать другую насадку для нашей мясорубки. Для этого напишем функцию `worker2` которая должна находить разность максимального и минимального значения внутри массива. Это можно интерпретировать как расстояние между минимумом и максимумом. Заметьте, что данная разность - всегда неотрицательное число. Затем используйте данную насадку как аргумент для функции mincer.


### Пример
```js
//worker
let arrOfArr = [[1, 2, 3], [4, 5, 6]];
mincer(arrOfArr, worker); // 15

arrOfArr = [[10, 10, 11], [20, 10]];
mincer(arrOfArr, worker); // 31

arrOfArr = [[0, 0, 0], [-1, -100]];
mincer(arrOfArr, worker); // 0

//worker2
arrOfArr = [[-10, -20, -40], [10, 20, 30]];
mincer(arrOfArr, worker2); // 30

arrOfArr = [[0, 0, 0], [-1, -99]];
mincer(arrOfArr, worker2); // 98
```
