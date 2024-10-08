- [Односвязный список](#односвязный-список)
  - [Определение узла односвязного списка](#определение-узла-односвязного-списка)
  - [Построение односвязного списка](#построение-односвязного-списка)
  - [Функция вывода элементов](#функция-вывода-элементов)
  - [Подсчёт длины списка](#подсчёт-длины-списка)
  - [Добавление элемента в конец списка](#добавление-элемента-в-конец-списка)
  - [Поиск элемента в односвязном списке](#поиск-элемента-в-односвязном-списке)
  - [Удаление элемента из односвязного списка](#удаление-элемента-из-односвязного-списка)
  - [Вставка элемента в односвязный список](#вставка-элемента-в-односвязный-список)
- [Двусвязный список](#двусвязный-список)
  - [Построение двусвязного списка вручную](#построение-двусвязного-списка-вручную)
  - [Вывод элементов двусвязного списка](#вывод-элементов-двусвязного-списка)
  - [Функция для вывода списка в обратном порядке:](#функция-для-вывода-списка-в-обратном-порядке)
  - [Функция для построения двусвязного списка из листа](#функция-для-построения-двусвязного-списка-из-листа)
  - [Функция для добавления элемента в конец:](#функция-для-добавления-элемента-в-конец)
  - [Функция добавления элемента в конец с использованием tail](#функция-добавления-элемента-в-конец-с-использованием-tail)

# Односвязный список

**Односвязный список** — это динамическая структура данных, состоящая из элементов, называемых узлами.  

Каждый узел содержит два поля:

1. Значение (value) — данные, которые хранятся в узле.
2. Ссылка на следующий узел (next) — указатель на следующий элемент в списке.
Последний элемент списка имеет указатель на ```None```, что означает конец списка.

## Определение узла односвязного списка

```python
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None
```

## Пример односвязного списка

Допустим, у нас есть список значений [3, 5, 7]. Это будет выглядеть так:

```python
3 --> 5 --> 7 --> None
```

- Узел 1: Значение = 3, Ссылка на следующий = 5
- Узел 2: Значение = 5, Ссылка на следующий = 7
- Узел 3: Значение = 7, Ссылка на следующий = None (конец списка)

## Построение односвязного списка

Мы будем добавлять узлы, связывая их друг с другом через атрибут .next.  

### Шаг 1: Создание первого узла (головы списка)

Мы начинаем с создания первого узла (головы) списка. Этот узел содержит значение, например, 1.

```python
head = ListNode(1)  # Голова списка, значение = 1
```

На данном этапе наш список состоит из одного узла, и его next указывает на None (конец списка).

```python
head (1) --> None
```

### Шаг 2: Добавление второго узла

Теперь добавим второй узел со значением, например, 2. Для этого создаем новый узел и устанавливаем next головы (первого узла) на этот новый узел.

```python
second_node = ListNode(2)  # Второй узел, значение = 2
head.next = second_node    # Связываем первый узел со вторым
```

Теперь наш список выглядит так:

```python
head (1) --> (2) --> None
```

### Шаг 3: Добавление третьего узла

Продолжим аналогичным образом: создадим третий узел со значением 3 и свяжем второй узел с ним.

```python
third_node = ListNode(3)   # Третий узел, значение = 3
second_node.next = third_node  # Связываем второй узел с третьим
```

```python
head (1) --> (2) --> (3) --> None
```

### Шаг 4: Добавление четвертого узла

Добавим еще один узел с числом 4 и привяжем его к третьему узлу:

```python
fourth_node = ListNode(4)  # Четвертый узел, значение = 4
third_node.next = fourth_node  # Связываем третий узел с четвертым
```

Теперь полный список:

```python
head (1) --> (2) --> (3) --> (4) --> None
```

#### Код создания списка

```python
# Шаг 1: Создание головы списка
head = ListNode(1)  # Голова списка, значение = 1
# Список выглядит так: 1 --> None

# Шаг 2: Добавление второго узла
second_node = ListNode(2)  # Второй узел, значение = 2
head.next = second_node    # Связываем первый узел со вторым
# Список выглядит так: 1 --> 2 --> None

# Шаг 3: Добавление третьего узла
third_node = ListNode(3)   # Третий узел, значение = 3
second_node.next = third_node  # Связываем второй узел с третьим
# Список выглядит так: 1 --> 2 --> 3 --> None

# Шаг 4: Добавление четвертого узла
fourth_node = ListNode(4)  # Четвертый узел, значение = 4
third_node.next = fourth_node  # Связываем третий узел с четвертым
# Список выглядит так: 1 --> 2 --> 3 --> 4 --> None
```

## Вывод элементов

В отличие от массива, где мы знаем его длину и можем получить доступ к элементам по индексу, односвязный список не предоставляет возможности прямого доступа к элементам через индекс. Чтобы вывести все элементы списка, нужно пройти по каждому узлу, начиная с головы, и выводить значения по очереди.  

Мы не можем просто написать несколько ```print``` команд, так как заранее неизвестно, сколько элементов находится в списке. Единственный способ получить доступ к каждому элементу — это последовательно переходить от одного узла к другому с помощью ссылки ```.next```, пока не достигнем конца списка (узел, где ```next == None```).

## Функция вывода элементов

Для этого мы напишем функцию, которая будет проходить по списку с помощью цикла ```while```. В каждой итерации цикла мы будем:

1. Выводить значение текущего узла.
2. Переходить к следующему узлу.

```python
def print_linked_list(head):
    current = head  # Начинаем с головы списка
    while current != None:  # Пока не достигнем конца списка
        print(current.val)  # Выводим значение текущего узла
        current = current.next  # Переходим к следующему узлу
```

### Пояснение работы цикла while и переходов

- В начале цикла ```current``` указывает на текущий узел, и мы выводим его значение через ```print(current.val)```.
- Затем выполняется команда ```current = current.next```. Это переменная ```current``` теперь будет указывать на следующий узел списка, так как каждый узел в односвязном списке содержит ссылку на следующий.
- Цикл повторяется до тех пор, пока current не станет равен ```None```, что указывает на конец списка.  

Таким образом, функция постепенно проходит через все узлы списка и выводит их значения.

### Как работает функция на практике

Допустим, у нас есть следующий список:

```python
head (1) --> (2) --> (3) --> (4) --> None
```

Мы вызываем функцию ```print_linked_list(head)```, перед началом цикла ```current``` указывает на узел со значением 1.

```python
(1) --> (2) --> (3) --> (4) --> None
 ↑
cur
```

Вот что происходит на каждой итерации цикла ```while```:

#### Итерация 1:

- current указывает на голову списка (узел с val = 1).
- Мы выводим current.val, то есть 1.
- Переходим к следующему узлу с помощью ```current = current.next```. Теперь current указывает на узел со значением 2.

```python
Выведено: 1

(1) --> (2) --> (3) --> (4) --> None
         ↑
        cur
```

#### Итерация 2:

- current теперь указывает на узел со значением 2.
- Мы выводим 2.
- Переходим к следующему узлу: ```current = current.next```. Теперь current указывает на узел со значением 3.

```python
Выведено: 2

(1) --> (2) --> (3) --> (4) --> None
                 ↑
                cur
```

#### Итерация 3:

- current теперь указывает на узел со значением 3.
- Мы выводим 3.
- Переходим к следующему узлу: ```current = current.next```. Теперь current указывает на узел со значением 4.

```python
Выведено: 3

(1) --> (2) --> (3) --> (4) --> None
                         ↑
                        cur

```

#### Итерация 4:

- current теперь указывает на узел со значением 4.
- Мы выводим 4.
- Переходим к следующему узлу: ```current = current.next```. Теперь current указывает на ```None``.

```python
Выведено: 4

(1) --> (2) --> (3) --> (4) --> None
                                 ↑
                                cur

```

#### Завершение цикла:

На этом этапе current указывает на None, что означает конец списка, и цикл завершится

## Подсчёт длины списка

Для того чтобы посчитать длину односвязного списка, нужно пройти по каждому узлу и на каждой итерации увеличивать счетчик на 1. Когда цикл дойдет до конца списка (то есть когда current станет равен ```None```), мы возвращаем значение счетчика.

```python
def get_linked_list_length(head):
    count = 0  # Изначально длина списка равна 0
    current = head  # Начинаем с головы списка
    while current != None:  # Пока не дойдем до конца списка
        count += 1  # Увеличиваем счетчик на 1
        current = current.next  # Переходим к следующему узлу
    return count  # Возвращаем длину списка

```

### Разбор работы функции на примере

Допустим, у нас есть следующий список:

```python
(1) --> (2) --> (3) --> (4) --> None
```

Мы вызываем функцию ```get_linked_list_length(head)```, и вот как изменяются значения переменных ```count``` и ```current``` на каждой итерации цикла:

#### Перед началом цикла:

- ```count = 0``` — длина списка еще не посчитана.
- ```current``` указывает на голову списка (узел со значением 1).
- 
```python
count = 0

(1) --> (2) --> (3) --> (4) --> None
 ↑
cur
```

#### Итерация 1:

- ```current``` указывает на узел со значением 1.
- Увеличиваем ```count```: ```count = 1```.
- Переходим к следующему узлу: ```current = current.next```.

```python
count = 1

(1) --> (2) --> (3) --> (4) --> None
         ↑
        cur
```

#### Итерация 2:

- ```current``` указывает на узел со значением 2.
- Увеличиваем ```count```: ```count = 2```.
- Переходим к следующему узлу: ```current = current.next```.

```python
count = 2

(1) --> (2) --> (3) --> (4) --> None
                 ↑
                cur
```

#### Итерация 3:

- ```current``` указывает на узел со значением 3.
- Увеличиваем ```count```: ```count = 3```.
- Переходим к следующему узлу: ```current = current.next```.

```python
count = 3

(1) --> (2) --> (3) --> (4) --> None
                         ↑
                        cur
```

#### Итерация 4:

- ```current``` указывает на узел со значением 4.
- Увеличиваем ```count```: ```count = 4```.
- Переходим к следующему узлу: ```current = current.next```.

```python
count = 4
(1) --> (2) --> (3) --> (4) --> None
                                 ↑
                                cur (None)
```

#### Завершение:

- Теперь ```current``` указывает на None, что означает конец списка.
- Цикл завершен, и мы возвращаем ```count = 4``` как длину списка.

## Добавление элемента в конец списка

Для того чтобы добавить элемент в конец списка, нужно пройти по списку, начиная с головы, пока не дойдем до последнего элемента (узел, где ```next == None```). После этого новый узел добавляется как следующий элемент последнего узла

## Функция для добавления элемента в односвязного списка конец

```python
def append_to_tail(head, value):
    new_node = ListNode(value)  # Создаем новый узел с переданным значением
    if head == None:  # Если список пуст, новый узел становится головой
        return new_node
    
    current = head  # Начинаем с головы
    
    while current.next != None:  # Проходим по списку до последнего узла
        current = current.next  # Переход к следующему узлу
    current.next = new_node  # Добавляем новый узел в конец списка
    
    return head  # Возвращаем голову списка
```

### Разбор работы функции на примере

Допустим, у нас есть следующий список:

```python
(1) --> (2) --> (3) --> None
```

Мы вызываем ```append_to_tail(head, 4)``` для добавления узла со значением 4 в конец списка.

#### Перед началом цикла

- Создаем новый узел со значением 4: ```new_node = ListNode(4)```.
- ```current``` указывает на голову списка (узел со значением 1).

```python
new_node = (4) --> None
current = (1)

(1) --> (2) --> (3) --> None
 ↑
cur

```

#### Итерация 1:

- ```current``` указывает на узел со значением 1.
- Переходим к следующему узлу: ```current = current.next```.

```python
current = (2)

(1) --> (2) --> (3) --> None
         ↑       ↑
        cur    cur.next 
```

#### Итерация 2:

- ```current``` указывает на узел со значением 2.
- Переходим к следующему узлу: ```current = current.next```.

```python
current = (3)

(1) --> (2) --> (3) --> None
                 ↑       ↑
                cur    cur.next 
```

#### Завершение цикла

- ```current``` указывает на узел со значением 3.
- Так как ```current.next == None```, это конец списка, цикл прерывается. Теперь в ```current``` лежит поселдний узел списка, 3.
- Добавляем новый узел: ```current.next = new_node ```.

```python
(1) --> (2) --> (3) --> (4) --> None
                 ↑       ↑
                cur    cur.next 

```

### Построение односвязного списка с помощью функции ```append_to_tail```

Теперь, используя функцию append_to_tail, создадим односвязный список с элементами [1, 2, 3, 4] и выведем его:

```python
# Определение класса узла
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

# Функция добавления элемента в конец списка
def append_to_tail(head, value):
    new_node = ListNode(value)
    if head == None:
        return new_node
    current = head
    while current.next != None:
        current = current.next
    current.next = new_node
    return head

# Функция для вывода элементов списка
def print_linked_list(head):
    current = head
    while current != None:
        print(current.val, end=" --> ")
        current = current.next
    print("None")

# Построение списка
head = ListNode(1)  # Создаем голову списка
head = append_to_tail(head, 2)  # Добавляем элемент 2
head = append_to_tail(head, 3)  # Добавляем элемент 3
head = append_to_tail(head, 4)  # Добавляем элемент 4

# Вывод списка
print_linked_list(head)

```

Вывод:

```python
1 --> 2 --> 3 --> 4 --> None
```

## Поиск элемента в односвязном списке

Чтобы найти элемент в односвязном списке, нужно пройти по каждому узлу, начиная с головы, и сравнивать значение каждого узла с искомым. Если мы находим узел с нужным значением, функция возвращает True. Если проходим по всему списку и не находим элемент, возвращаем False.

```python
def search_in_linked_list(head, value):
    current = head  # Начинаем с головы списка
    
    while current != None:  # Пока не дойдем до конца списка
        if current.val == value:  # Если значение узла совпадает с искомым
            return True  # Элемент найден, возвращаем True
        current = current.next  # Переходим к следующему узлу
    
    return False  # Если дошли до конца списка и не нашли элемент, возвращаем False
```

### Как работает функция по этапам

Допустим, у нас есть следующий список:

```python
(1) --> (2) --> (3) --> (4) --> None
```

Мы вызываем ```search_in_linked_list(head, 3)``` для поиска элемента со значением 3.

#### Перед началом цикла:

```current``` указывает на голову списка (узел со значением 1).

```python
(1) --> (2) --> (3) --> (4) --> None
 ↑
cur
```

#### Итерация 1:

- ```current``` указывает на узел со значением 1.
- Так как ```current.val != 3```, продолжаем поиск.
- Переходим к следующему узлу: ```current = current.next```.

```python
(1) --> (2) --> (3) --> (4) --> None
         ↑
        cur
```

#### Итерация 2:

- ```current``` указывает на узел со значением 2.
- Так как ```current.val != 3```, продолжаем поиск.
- Переходим к следующему узлу: ```current = current.next```.

```python
(1) --> (2) --> (3) --> (4) --> None
                 ↑
                cur
```

#### Итерация 3:

- ```current``` указывает на узел со значением 3.
- Так как ```current.val == 3```, возвращаем ```True``` — элемент найден.

```python
(1) --> (2) --> (3) --> (4) --> None
                 ↑
                cur

Результат: True
```

Если бы элемент не был найден в списке (например, мы искали бы 5), функция продолжила бы проходить по узлам до тех пор, пока current не стал бы равен None, и в этом случае вернула бы False.

## Удаление элемента из односвязного списка

Чтобы удалить элемент из односвязного списка, нужно:

1. Найти узел, который нужно удалить.
2. Перекинуть ссылку с предыдущего узла на следующий узел после удаляемого, чтобы разорвать связь с узлом, который удаляем.

**Схематичное изображение удаления:**

Допустим, у нас есть список:

```python
(1) --> (2) --> (3) --> (4) --> None
```
Мы хотим удалить элемент со значением 3.

1. Сначала находим узел со значением 3.
2. Связываем предыдущий узел (2) с узлом после удаляемого (4), чтобы узел 3 больше не был связан с цепочкой.

Важно помнить о ссылке на предыдущий узел, потому что мы должны перекинуть его ссылку на следующий узел после удаляемого узла. Переменная prev будет хранить указатель на предыдущий узел, а переменная current будет указывать на текущий узел, который мы проверяем.

```python
До удаления:
(1) --> (2) --> (3) --> (4) --> None
         ↑       ↑       ↑
        prev    cur    cur.next

prev.next = cur.next

После удаления:
(1) --> (2) --------> (4) --> None
         ↑             ↑
       prev          cur.next

```

1. Сначала находим узел со значением 3, используя переменные ```current``` (текущий узел) и паралельно храним ```prev``` (предыдущий узел).

2. Когда находим узел со значением 3 (```current == 3```), перекидываем ссылку с узла 2 (предыдущего ```prev```) на узел 4 (следующего после удаляемого узла ```prev.next = current.next```). Т.е. теперь следующий узел после ```prev``` (2) это ```current.next``` (4)

```python
def delete_node(head, value):
    # Если список пуст, возвращаем None
    if head == None:
        return None
    
    # Если элемент для удаления - это голова списка
    if head.val == value:
        return head.next  # Возвращаем следующий узел, который станет новой головой

    # Инициализируем указатели на текущий и предыдущий узлы
    current = head
    prev = None  # На первом этапе предыдущий узел не существует

    # Проходим по списку, пока не найдем элемент для удаления
    while current != None:
        
        if current.val == value:  # Если текущий узел содержит искомое значение
            prev.next = current.next  # Перекидываем ссылку с предыдущего узла
            return head  # Возвращаем голову списка после удаления элемента
        
        prev = current  # Сохраняем текущий узел как предыдущий
        current = current.next  # Переходим к следующему узлу

    # Если элемент не был найден, возвращаем неизмененную голову
    return head
```

Основная идея в том, что мы перемещаемся по списку с двумя указателями: один хранит текущий узел (current), а другой — предыдущий (prev). Когда мы находим узел, который нужно удалить, мы используем prev для изменения связи между узлами.

### Пример работы функции

Допустим, мы хотим удалить элемент со значением 3 из списка:

```python
(1) --> (2) --> (3) --> (4) --> None
```

Мы вызываем ```delete_node(head, 3)```. Давайте рассмотрим пошагово, как работает функция:

#### Перед началом цикла:

- ```current``` указывает на голову списка (узел со значением 1).
- ```prev``` равен ```None```, так как у головы нет предыдущего узла.

```python
current = (1)
prev = None

(1) --> (2) --> (3) --> (4) --> None
↑
cur
```

#### Итерация 1:
- ```current``` указывает на узел со значением 1.
- Так как ```current.val != 3```, продолжаем искать.
- Сохраняем ```current``` в переменную ```prev```.
- Переходим к следующему узлу: ```current = current.next```.

```python
current = (2)
prev = (1)

(1) --> (2) --> (3) --> (4) --> None
 ↑       ↑
prev    cur
```

#### Итерация 2:
- ```current``` указывает на узел со значением 2.
- Так как ```current.val != 3```, продолжаем искать.
- Сохраняем ```current``` в переменную ```prev```.
- Переходим к следующему узлу: ```current = current.next```.

```python
current = (3)
prev = (2)

(1) --> (2) --> (3) --> (4) --> None
         ↑       ↑
        prev    cur
```

#### Итерация 3:
- ```current``` указывает на узел со значением 3.
- Так как ```current.val == 3```, мы нашли элемент для удаления.
- Сохраняем ```current``` в переменную ```prev```.
- Используем prev для перекидывания ссылки: ```prev.next = current.next```.

```python
current = (3)
prev = (2)

(1) --> (2) --> (3) --> (4) --> None
         ↑       ↑       ↑
        prev    cur    cur.next

prev.next = current.next

(1) --> (2) --------> (4) --> None
         ↑             ↑
        prev         prev.next
        (ссылка перекинута через узел 3)
```

#### Завершение

Теперь узел со значением 3 больше не связан со списком. Ни один из узлов списка больше не указывает на узел со значением 3.

### Пример использования функции

Теперь давайте создадим список, удалим из него элемент и выведем результат:

```python
# Определение класса узла
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

# Функция для добавления элемента в конец списка
def append_to_tail(head, value):
    new_node = ListNode(value)
    if head == None:
        return new_node
    current = head
    while current.next != None:
        current = current.next
    current.next = new_node
    return head

# Функция для вывода элементов списка
def print_linked_list(head):
    current = head
    while current != None:
        print(current.val, end=" --> ")
        current = current.next
    print("None")

# Функция для удаления узла
def delete_node(head, value):
    if head == None:
        return None
    if head.val == value:
        return head.next
    current = head
    prev = None
    while current != None:
        if current.val == value:
            prev.next = current.next
            return head
        prev = current
        current = current.next
    return head

# Построение списка
head = ListNode(1)
head = append_to_tail(head, 2)
head = append_to_tail(head, 3)
head = append_to_tail(head, 4)

# Вывод исходного списка
print("Исходный список:")
print_linked_list(head)

# Удаление элемента со значением 3
head = delete_node(head, 3)

# Вывод списка после удаления
print("\nСписок после удаления элемента 3:")
print_linked_list(head)
```

**Результат:**

```python
Исходный список:
1 --> 2 --> 3 --> 4 --> None

Список после удаления элемента 3:
1 --> 2 --> 4 --> None
```

## Вставка элемента в односвязный список

Для вставки элемента в односвязный список после заданного узла нам нужно:

1. Найти узел, после которого хотим вставить новый элемент.
2. Создать новый узел.
3. Перекинуть ссылки так, чтобы новый узел стал частью цепочки, а текущие связи не нарушились.


### Схематичное изображение вставки:

Допустим, у нас есть список:

```python
(1) --> (2) --> (3) --> (4) --> None
```
Мы хотим вставить новый элемент со значением 5 после узла со значением 2.

**Шаг 1.**  
Сначала находим узел со значением 2. Мы перемещаем указатель current по списку, пока не дойдем до узла со значением 2.
```python
(1) --> (2) --> (3) --> (4) --> None
         ↑
        cur
```

**Шаг 2.**  
Создаем новый узел new_node со значением 5. Пока что этот узел не связан с остальными узлами списка.

```python
(1) --> (2) --> (3) --> (4) --> None
         ↑
        cur

new_node = (5) --> None
```

**Шаг 3.**  
Теперь мы связываем новый узел (```new_node```) с тем, что был следующим узлом после ```current```, то есть с узлом со значением 3.  
Это делается через команду ```new_node.next = current.next```.

```python
(1) --> (2) --> (3) --> (4) --> None
         ↑       ^ 
        cur      |
                 |
                (5) 
                 ↑
              new_node
```

**Шаг 4.**  
Перекидываем ссылку с ```current``` на ```new_node```. Перекидываем ссылку с узла 2 на новый узел 5, а уже новый узел 5 ссылается на узел 3.  
Это делается через команду ```current.next = new_node```.

```python
(1) --> (2) --|     (3) --> (4) --> None
         ↑    |      ^ 
        cur   |      |
              |      |
              ----->(5) 
                     ↑
                  new_node
```

Теперь новый узел 5 успешно вставлен после узла 2, и все связи в списке остаются корректными.

```python
(1) --> (2) --> (5) --> (3) --> (4) --> None
         ↑       ↑
        cur   new_node
```


### Функция вставки

```python
def insert_after_node(head, target_value, new_value):
    # Инициализируем указатель на текущий узел, начиная с головы
    current = head

    # Ищем узел, после которого нужно вставить новый элемент
    while current != None:
        if current.val == target_value:
            # Создаем новый узел с новым значением
            new_node = ListNode(new_value)
            # Перекидываем ссылки
            new_node.next = current.next  # Новый узел указывает на следующий узел
            current.next = new_node  # Текущий узел указывает на новый узел
            return head  # Возвращаем обновленную голову списка
        current = current.next  # Переходим к следующему узлу

    # Если узел с target_value не найден, возвращаем неизмененную голову
    return head
```

- ```target_value``` - значение узла после, которого нужно вставить новый узел
- ```new_value``` - значение новго узла
- ```current``` — это указатель на текущий узел, который мы проверяем, чтобы найти узел, после которого нужно вставить новый элемент
- ```new_node``` — новый узел, который мы создаем и вставляем в список

Функция последовательно проходит по списку с помощью указателя ```current```, пока не находит узел, соответствующий значению ```target_value```. После этого она создает новый узел и правильно устанавливает ссылки, чтобы включить его в список.

# Двусвязный список

**Двусвязный список** — это структура данных, состоящая из узлов, каждый из которых хранит три элемента:

- **Значение (```value```)** — данные, которые хранятся в узле.
- **Ссылка на следующий узел (```next```)** — указатель на следующий узел в списке.
- **Ссылка на предыдущий узел (```prev```)** — указатель на предыдущий узел в списке.

В двусвязном списке можно легко перемещаться как вперед, так и назад по элементам, благодаря тому, что каждый узел знает не только о следующем узле, но и о предыдущем.

Пример класса узла двусвязного списка:

```python
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None
        self.prev = None
```

## Построение двусвязного списка вручную

Теперь поэтапно создадим двусвязный список без использования функций, просто связывая узлы через ```next``` и ```prev```.

**Шаг 1: Создание первого узла (головы списка)**

Начнем с создания первого узла, который будет головой списка.

```python
head = ListNode(1)  # Голова списка, значение = 1
```

Пока что у нас есть только один узел, который никуда не ссылается (оба указателя ```next``` и ``prev`` равны ```None```).

```python
None <-- (1) --> None
          ↑ 
         head
```

**Шаг 2: Добавление второго узла**

Теперь добавим второй узел со значением 2 и правильно свяжем его с первым узлом. Первый узел (head) будет ссылаться на второй через ```next```, а второй узел будет ссылаться на первый через ```prev```.

```python
second_node = ListNode(2)  # Второй узел, значение = 2
head.next = second_node  # Первый узел указывает на второй
second_node.prev = head  # Второй узел указывает на первый
```

Теперь структура списка такова:

```python
None <--  (1) <--> (2) --> None
           ↑        
          head
```

**Шаг 3: Добавление третьего узла**

Добавим третий узел со значением 3 и снова свяжем его с предыдущим узлом (```second_node```).

```python
third_node = ListNode(3)  # Третий узел, значение = 3
second_node.next = third_node  # Второй узел указывает на третий
third_node.prev = second_node  # Третий узел указывает на второй
```

Теперь структура списка выглядит следующим образом:

```python
None <--  (1) <--> (2) <--> (3) --> None
           ↑        
          head
```

**Шаг 4: Добавление четвертого узла**

Добавим четвертый узел со значением 4 и свяжем его с третьим узлом.

```python
fourth_node = ListNode(4)  # Четвертый узел, значение = 4
third_node.next = fourth_node  # Третий узел указывает на четвертый
fourth_node.prev = third_node  # Четвертый узел указывает на третий
```

Теперь полный список выглядит так:
```python
None <--  (1) <--> (2) <--> (3) <--> (4) --> None
           ↑ 
          head
```

### Код создания двусвязного списка

```python
# Определение узла двусвязного списка
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None
        self.prev = None

# Шаг 1: Создание головы списка (первый узел)
head = ListNode(1)  # Узел со значением 1
# Структура: None <-- (1) --> None

# Шаг 2: Добавление второго узла
second_node = ListNode(2)  # Узел со значением 2
head.next = second_node  # Первый узел указывает на второй
second_node.prev = head  # Второй узел указывает на первый
# Структура: None <-- (1) <--> (2) --> None

# Шаг 3: Добавление третьего узла
third_node = ListNode(3)  # Узел со значением 3
second_node.next = third_node  # Второй узел указывает на третий
third_node.prev = second_node  # Третий узел указывает на второй
# Структура: None <-- (1) <--> (2) <--> (3) --> None

# Шаг 4: Добавление четвертого узла
fourth_node = ListNode(4)  # Узел со значением 4
third_node.next = fourth_node  # Третий узел указывает на четвертый
fourth_node.prev = third_node  # Четвертый узел указывает на третий
# Структура: None <-- (1) <--> (2) <--> (3) <--> (4) --> None
```

## Вывод элементов двусвязного списка

```python
def print_doubly_linked_list(head):
    current = head  # Начинаем с головы
    while current != None:  # Проходим по списку, пока не дойдем до конца
        print(current.val, end=" <--> ")
        current = current.next  # Переходим к следующему узлу
    print("None")
```

### Пример использования

```python
# Определение класса узла двусвязного списка
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None
        self.prev = None

def print_doubly_linked_list(head):
    current = head  # Начинаем с головы
    while current != None:  # Проходим по списку, пока не дойдем до конца
        print(current.val, end=" <--> ")
        current = current.next  # Переходим к следующему узлу
    print("None")

# Построение списка
head = ListNode(1)
second_node = ListNode(2)
third_node = ListNode(3)
fourth_node = ListNode(4)

# Связываем узлы
head.next = second_node
second_node.prev = head
second_node.next = third_node
third_node.prev = second_node
third_node.next = fourth_node
fourth_node.prev = third_node

# Вывод списка
print_doubly_linked_list(head)
```

**Результат:**

```python
1 <--> 2 <--> 3 <--> 4 <--> None
```


## Функция для вывода списка в обратном порядке:

Для того чтобы вывести двусвязный список в обратном порядке, мы должны сначала дойти до конца списка, а затем идти в обратном направлении, используя указатели prev (которые указывают на предыдущие узлы).

```python
def print_reverse_doubly_linked_list(head):
    current = head
    
    # Сначала доходим до конца списка
    while current.next != None:
        current = current.next

    # Теперь идем в обратном порядке, пока не дойдем до начала списка
    while current != None:
        print(current.val, end=" <--> ")
        current = current.prev  # Переходим к предыдущему узлу

    print("None")
```

**Пояснение:**

- Первый цикл находит последний элемент списка, идя вперед через next.
- Второй цикл идет в обратном порядке через указатели prev, выводя элементы от конца к началу списка.

### Пример использования

```python
# Определение класса узла двусвязного списка
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None
        self.prev = None

# Построение списка
head = ListNode(1)
second_node = ListNode(2)
third_node = ListNode(3)
fourth_node = ListNode(4)

# Связываем узлы
head.next = second_node
second_node.prev = head
second_node.next = third_node
third_node.prev = second_node
third_node.next = fourth_node
fourth_node.prev = third_node

# Вывод списка в обратном порядке
print_reverse_doubly_linked_list(head)
```

**Результат:**

```python
4 <--> 3 <--> 2 <--> 1 <--> None
```

## Функция для построения двусвязного списка из листа

Чтобы построить двусвязный список из обычного Python списка (листа), мы будем создавать узлы для каждого элемента листа и связывать их между собой через указатели next и prev.

```python
def build_doubly_linked_list(lst):
    if not lst:  # Если лист пустой, возвращаем None
        return None
    
    # Создаем голову списка с первым элементом листа
    head = ListNode(lst[0])
    current = head
    
    # Проходим по остальным элементам листа и строим узлы
    for value in lst[1:]:
        new_node = ListNode(value)  # Создаем новый узел
        current.next = new_node  # Устанавливаем связь с следующим узлом
        new_node.prev = current  # Устанавливаем обратную связь с предыдущим узлом
        current = new_node  # Двигаемся к новому узлу
        
    return head  # Возвращаем голову списка
```

### Объяснение работы функции

- Проверка на пустой список:  
```if not lst:```: Если входной список пустой (lst пуст), функция сразу возвращает ```None```, так как нет элементов для построения списка.

- Создание головы списка:
  - ```head = ListNode(lst[0])```: Создаем первый узел списка с первым элементом входного списка ```lst[0]```. Этот узел становится головой двусвязного списка.
  - ```current = head```: Инициализируем указатель current, который будет использоваться для отслеживания текущего узла при построении списка.

- Итерация по оставшимся элементам списка:  
  ```for value in lst[1:]:```: Проходим по элементам входного списка, начиная со второго элемента (```lst[1:]```).
  - Создание нового узла:
    - ```new_node = ListNode(value)```: Создаем новый узел с текущим значением value.
  - Установка связей между узлами:
    - ```current.next``` = new_node: Устанавливаем ссылку next текущего узла current на новый узел new_node.
    - ```new_node.prev = current```: Устанавливаем ссылку prev нового узла new_node на текущий узел current.
  - Переход к новому узлу:
    - ```current = new_node```: Обновляем указатель current, чтобы он указывал на только что созданный узел new_node.

- Возврат головы списка:
  - ```return head```: После завершения цикла возвращаем голову двусвязного списка head.

## Функция для добавления элемента в конец:

```python
def append_to_tail(head, val):
    # Создаем новый узел с переданным значением
    new_node = ListNode(val)
    
    # Если список пуст, новый узел становится головой и хвостом
    if head == None:
        return new_node
    
    # Идем до конца списка, начиная с головы
    current = head
    while current.next != None:
        current = current.next
    
    # Устанавливаем связи для нового узла
    current.next = new_node
    new_node.prev = current
    
    # Возвращаем неизмененную голову списка
    return head
```

### Пример использования

```python
# Инициализация списка с одним элементом
head = ListNode(1)

# Добавление элементов в конец списка
head = append_to_tail(head, 2)
head = append_to_tail(head, 3)
head = append_to_tail(head, 4)

# Вывод двусвязного списка
print_doubly_linked_list(head)
```

**Результат:**

```python
1 <--> 2 <--> 3 <--> 4 <--> None
```

## Функция добавления элемента в конец с использованием tail

Если в функцию передаются указатели на голову (head) и хвост (tail) двусвязного списка, задача упрощается. Мы можем сразу добавить элемент после хвоста, обновив указатели на новый узел. После этого хвост нужно обновить, чтобы он указывал на новый последний элемент.

```python
def append_to_tail(head, tail, val):
    # Создаем новый узел с переданным значением
    new_node = ListNode(val)
    
    # Если список пуст (head и tail равны None), новый узел становится головой и хвостом
    if head == None and tail == None:
        return new_node, new_node
    
    # Связываем новый узел с текущим хвостом
    tail.next = new_node
    new_node.prev = tail
    
    # Обновляем хвост
    tail = new_node
    
    # Возвращаем неизмененную голову и обновленный хвост
    return head, tail
```

**Пояснение:**

1. Создаем новый узел с переданным значением.
2. Если список пуст (оба указателя head и tail равны None), то новый узел становится и головой, и хвостом списка. Функция возвращает два указателя: на голову и хвост.
3. Если список не пуст, мы связываем текущий хвост с новым узлом: обновляем указатели next у хвоста и prev у нового узла.
4. Обновляем указатель на хвост, чтобы он указывал на новый узел.
5. Функция возвращает указатели на голову (неизмененную) и хвост (обновленный).
