﻿# Лабораторная №3
### Кто такой Чарльз Хоар? Чем он известен?
Английский учёный-информатик. в 1960 году в МГУ разработал алгоритм быстрой сортировки, который используется и по сей день.
### Общее описание метода Хоара
Алгоритм является рекурсивным. На каждом вызове функции разбиваем массив на две части. Причём все элементы одной половины должны быть меньше опорного элемента, а в другой половине больше(или наоборот). 
### Алгоритм метода Хоара
Разбиваем массив относительно опорного элемента так, чтобы все элементы одной половины были меньше любого элемента другой:
````c++
do
{
    while(arr[leftElem] < separator) //определяем левую часть
    {
        leftElem++;
    }
    while(arr[rightElem] > separator) //определяем праву часть
    { 
        rightElem--;
    }

    if(leftElem <= rightElem) //если массив разделён не полностью
    {
        if(arr[leftElem] > arr[rightElem])//если элементы не в своей половинке, то меняем их местами
        {
            int  supportElem = arr[leftElem];
            arr[leftElem] = arr[rightElem];
            arr[rightElem] = supportElem;
        }
        leftElem++;
        rightElem--;
    }
} while(leftElem <= rightElem);
````

Если половинки не отсортированы так же рекурсивно разбиваем их на части относительно нового опорного элемента:
````c++
if(leftElem < top) //рекурсивные вызовы
xoaraSort(arr, leftElem, top);
if(rightElem > low)
xoaraSort(arr, low, rightElem);
````
### Как происходит выбор опорного пункта
Лучший случай тот, когда в качестве опорного элемента выбирается медиана всех элементов. Однако её трудно вычислить, поэтому обычно в качестве опорного элемента берётся тот, который находится по-середине:
````c++
int  separator = arr[(low + top) / 2];
````
### Разбиение Ломуто
В качестве опорного элемента выбирается последний элемент. На каждом шаге ищется элемент больший (или меньший) опорного и ставится перед (или после) ним.
Алгоритм прост, но его эффективность низкая.
### Разбиение Хоара
В качестве опорного элемента выбирается средний элемент. Далее используются два дополнительных индекса, один из которых указывает на начало массива, другой на его конец. Если элементы этих индексов расположены в правильной половинке ( в левой - меньшие, в правой - большие или наоборот), то они сдвигаются друг к другу (левый ++, правый --), если не в правильной, то элементы с этими индексами меняются местами, а индексы так же сдвигаются дальше (левый ++, правый --). 
В среднем с таким разбиением требуется в 3 раза меньше операций, чем с разбиением Ломуто.

### Достоинства и недостатки
(+):
+ Один из самых быстродействующих на практике.
+ Может использоваться на связных списках.

(-): 
+ Нестабилен, так как может привести к переполнению стека вызовами.
### Интересные факты метода Хоара
В общем случае сложность алгоритма О(N*logN), а при разбиении на три части О(N).
В худшем случае О(N^2).

