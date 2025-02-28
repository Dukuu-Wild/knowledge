---
tags: [python, программирование]
---
# 🐍 30 уловок на языке Python, которые сделают вас лучшим программистом

[eFusion](https://proglib.io/u/eFusion) 14 февраля 2021

Существует множество облегчающих жизнь программиста на Python лайфхаков. Даже если вы уже овладели языком, вы все равно должны это прочитать.

![](https://media.proglib.io/posts/2021/02/14/7d540c2f837e7ae5a45701f5bc90750e.png)

_Перевод публикуется с сокращениями, автор [оригинальной статьи](https://medium.com/pythonland/30-python-language-tricks-that-will-make-you-a-better-coder-f08f811a7b0f) – Erik van Baaren._

## 1. Многоточие в Python

Многоточие Python – это последовательность из трех точек, часто используемая в естественных языках. Но чего вы, возможно, не знаете – это еще и валидный объект в Python:

``` py
>>> ...
Ellipsis
```

Применяется он преимущественно в операциях нарезки матриц в NumPy. Однако можно использовать его вместо обычного pass в качестве плэйсхолдера в функции, которую еще не реализовали:

``` py
def my_awesome_func():
...
```

Вот валидный код Python, и выглядит он теперь не так уж плохо.

## 2. Data classes

Начиная с версии 3.7, Python поставляется с классами данных. У них есть несколько преимуществ по сравнению с обычными классами или другими альтернативами:

* возврат нескольких значений или словарей;
* класс данных требует минимального количества кода;
* возможность сравнения классов данных;
* возможность распечатать класс данных для отладки при помощи \_\_repr\_\_;
* снижение вероятности ошибок в связи с требованием класса данных type hints.  

Пример класса данных в работе:

``` py
from dataclasses import dataclass

@dataclass
class Card:
rank: str
suit: str

card = Card("Q", "hearts")

print(card == card)
# True

print(card.rank)
# 'Q'

print(card)
Card(rank='Q', suit='hearts')
```

## 3. The Zen of Python

Одним из самых ранних Python pep является [PEP-20](https://www.python.org/dev/peps/pep-0020/). Это список из 19 тезисов по программированию на Python, который называется «The Zen of Python». Данные правила датируются 2004 годом и, в свою очередь, основаны на [PEP-8](https://www.python.org/dev/peps/pep-0008/).

Такая пасхалочка уже давно присутствует в Python и перечисляет набор правил:

![](https://media.proglib.io/posts/2021/02/13/db647450f47136d8a0f76be67bc7e7e5.png)

Так что пока у вас есть Python REPL, можете просматривать эти правила на экране.

## 4. Анонимные функции

Иногда именованию функции не стоит уделять особого внимания. Например, если вы уверены, что она будет использована только раз. Для таких случаев Python предлагает применять анонимные функции, также называемые лямбда-функциями.

![](https://media.proglib.io/posts/2021/02/13/4e09b52966bcb26754b31204e76eaf63.jpg)

Лямбда-функция может быть назначена переменной, создавая краткий способ определения функции:

``` py
>>> add_one = lambda x: x + 1
>>> add_one(3)
4
```

Это становится более интересным, когда необходимо использовать функцию в качестве аргумента. В таких случаях она часто используется только один раз. Как известно, map применяет функцию ко всем элементам итерируемого объекта. Мы можем использовать лямбду при вызове map:

``` py
>>> numbers = [1, 2, 3, 4]
>>> times_two = map(lambda x: x * 2, numbers)
>>> list(times_two)
[2, 4, 6, 8]
>>>
```

Этот кусок кода встречается часто. Например, когда требуется применить операцию к каждому элементу итеративного объекта. В данной ситуации использование map() в сочетании с лямбда-функцией является кратким и эффективным.

## 5. List Comprehensions

List comprehension может заменить неэстетичные циклы, используемые для заполнения списка. Синтаксис выглядит следующим образом:

``` py
[ expression for item in list if conditional ]
```

Простейший пример заполнения списка последовательностью чисел:

``` py
mylist = [i for i in range(10)]
print(mylist)
# [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

Поскольку здесь можно использовать выражения, вам доступна работа с математикой:

``` py
squares = [x**2 for x in range(10)]
print(squares)
# [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

Вызов внешней функции:

``` py
def some_function(a):
return (a + 5) / 2

my_formula = [some_function(i) for i in range(10)]
print(my_formula)
# [2.5, 3.0, 3.5, 4.0, 4.5, 5.0, 5.5, 6.0, 6.5, 7.0]
```

И, наконец, вы сможете использовать «if» для фильтрации списка. В этом случае будут сохранены только те значения, которые делятся на 2:

``` py
filtered = [i for i in range(20) if i%2==0]
print(filtered)
# [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
```

## 6. Замена переменных на месте

![](https://media.proglib.io/posts/2021/02/13/5cacb9d8b8bd62be560f0e1a2ed270df.png)

Этот аккуратный трюк поможет сэкономить несколько строк кода:

``` py
a = 1
b = 2
a, b = b, a
print (a)
# 2
print (b)
# 1
```

## 7\. Форматирование именованных строк

Такую штуку используют нечасто, но если данные уже находятся в словаре, для форматирования именованных строк пригодится следующий прием:

![](https://media.proglib.io/posts/2021/02/13/f4d92beda2a9e2087645a5e500cecb51.png)

Вы даже можете использовать функцию locals(), но в последних версиях Python придется обращаться к f-строкам следующим образом:

![](https://media.proglib.io/posts/2021/02/13/cea1eccaf756a5308853f6211f0a7603.png)

## 8. Nested list comprehensions

Помните основной синтаксис list comprehensions?

``` py
[ expression for item in list if conditional ]
```

Если **expression** может быть любым валидным выражением Python, оно также может быть и другим list comprehension. Это полезно, когда необходимо создать матрицу:

``` py
>>> [ [j for j in range(3)] for i in range(4) ]
[ [0, 1, 2], [0, 1, 2], [0, 1, 2], [0, 1, 2] ]
```

Или, если хотите «разгладить» предыдущую матрицу:

``` py
>>> [value
  for sublist in m
  for value in sublist]
[0, 1, 2, 0, 1, 2, 0, 1, 2, 0, 1, 2]
```

Первая часть цикла по матрице m, а вторая – цикл по элементам каждого вектора.

## 9. Обязательные аргументы

Для принудительного использования аргументов ставьте символ звездочки перед ними, заставляя все аргументы стать ключевыми:

``` py
>>> def f(*, a, b):
... print(a, b)
...
>>> f(1, 2)
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
TypeError: f() takes 0 positional
arguments but 2 were given
>>> f(a=1, b=2)
1 2
>>>
```

## 10. Использование подчеркивания в REPL

Вы можете получить результат последнего выражения в Python REPL с помощью оператора подчеркивания, например, в Python REPL это выглядит следующим образом:

``` py
>>> 3 * 3
9
>>> _ + 3
12
```

Прием работает и в оболочке IPython.

## 11. Проверка необходимой версии Python

Чтобы ваши пользователи не могли запустить скрипт в несовместимой версии, в коде стоит проверить наличие актуальной версии Python. Проведите простую проверку:

``` py
if not sys.version_info > (2, 7):
   # berate your user for running a 10 year
   # python version
elif not sys.version_info >= (3, 5):
   # Kindly tell your user (s)he needs to upgrade
   # because you're using 3.5 features
```

## 12. Декорируем функции

Декоратор – это обертка вокруг функции, которая определенным образом изменяет ее поведение. Существуют варианты использования декораторов, и вы, возможно, уже применяли их раньше при работе с такими фреймворками, как Flask.

Давайте создадим собственного декоратора:

``` py
def print_argument(func):
def wrapper(the_number):
print("Argument for", 
  func.__name__, 
  "is", the_number)
return func(the_number)
return wrapper
@print_argument
def add_one(x):
return x + 1
print(add_one(1))
```

Внутри **print\_argument** мы определяем функцию-обертку. Она выводит аргумент и имя вызываемой функции, выполняет фактическую функцию и возвращает ее результат, как если бы функция вызывалась «обычно».

С помощью **@print\_argument** мы применяем наш декоратор к функции. Декоратор может быть повторно использован и для других функций.

Давайте создадим собственного декоратора:

``` py
Argument for add_one is 1
2
```

## 13. Возврат нескольких значений

Функции в Python могут возвращать более одной переменной без применения словаря, списка или класса. Это работает так:

``` py
def get_user(id):
# fetch user from database
# ....
return name, birthdate

name, birthdate = get_user(4)
```

Здесь возвращается кортеж. С тем же эффектом можно было бы написать **return (name, birthdate)**.

Это нормально для ограниченного количества возвращаемых значений. Но все, что превышает 3 значения, должно быть помещено в класс (data).

## 14. Объединение словарей

Начиная с Python 3.5, стало проще объединять словари.

``` py
dict1 = { 'a': 1, 'b': 2 }
dict2 = { 'b': 3, 'c': 4 }
merged = { **dict1, **dict2 }

print (merged)
# {'a': 1, 'b': 3, 'c': 4}

# Python >= 3.9 only
merged = dict1 | dict2

print (merged)
# {'a': 1, 'b': 3, 'c': 4}
```

Если встречаются дублирующиеся ключи – в первом словаре они будут перезаписаны.

## 15. Нарезка списка

Синтаксис нарезания таков:

``` py
a[start:stop:step]
```

**Start**, **stop** и **step** необязательны. У них есть дефолтные значения, которые активируются, если не заполнить параметры:

* 0 для **start**;
* конец списка для **stop**;
* 1 для **step**.  

Вот несколько примеров:

``` py
# We can easily create a new list from 
# the first two elements of a list:
first_two = [1, 2, 3, 4, 5][0:2]
print(first_two)
# [1, 2]

# And if we use a step value of 2, 
# we can skip over every second number
# like this:
steps = [1, 2, 3, 4, 5][0:5:2]
print(steps)
# [1, 3, 5]

# This works on strings too. In Python,
# you can treat a string like a list of
# letters:
mystring = "abcdefdn nimt"[::2]
print(mystring)
# 'aced it'
```

## 16. Использование памяти

С помощью **sys.getsizeof()** можно проверить использование памяти объектом:

``` py
import sys

mylist = range(0, 10000)
print(sys.getsizeof(mylist))
# 48
```

Огромный список всего 48 байт, потому что функция range возвращает класс, который ведет себя как список. В вопросе памяти range эффективнее, чем использование актуального списка чисел.

``` py
import sys

myreallist = [x for x in range(0, 10000)]
print(sys.getsizeof(myreallist))
# 87632
```

## 17. Использование \* и \*\* для распаковки аргументов функций

Некоторые функции требуют длинного списка аргументов. Этого следует избегать (например, с помощью классов данных), хотя это не всегда зависит от вас. Существует другой вариант – создать словарь с именованными аргументами и передать его функции. Так ваш код станет более читабельным.

Распаковать словарь можно, используя префикс \*\*:

``` py
>>> def f(a, b):
... print(a, b)
...
>>> args = { "a": 1, "b": 2 }
>>> f(**args)
1 2
```

Аналогично можно использовать \* для распаковки массива и передачи его содержимого в качестве аргументов функции:

``` py
>>> def f(a, b, c):
...print(a, b, c)
...
>>> l = [1, 2, 3]
>>> f(*l)
1 2 3
```

## 18. Строка – заголовок

Если хотите быстро получить красивый заголовок, сделайте так:

``` py
mystring = "10 awesome python tricks"
print(mystring.title())
'10 Awesome Python Tricks'
```

## 19. Разбиение строки в список

Вы можете разбить строку на список строк. В этом случае разбиение происходит по символу пробела:

``` py
mystring = "The quick brown fox"
mylist = mystring.split(' ')
print(mylist)
# ['The', 'quick', 'brown', 'fox']
```

Чтобы разделить по пустому месту, не нужно передавать в **split** никаких аргументов – используйте **mystring.split()**.

Split также имеет второй параметр, называемый **maxsplit**, который определяет максимальное количество разбиений. По умолчанию он равен -1 (без ограничений). Вот пример, с ограничением разбиения на 1:

``` py
>>> mystring.split(' ', 1)
['The', 'quick brown fox']
```

## 20. Создание строки из списка строк

Создание строки из списка и установка пробелов между каждым словом:

``` py
mylist = ['The', 'quick', 'brown', 'fox']
mystring = " ".join(mylist)
print(mystring)
# 'The quick brown fox'
```

Все сводится к тому, что функция **String.join()** может присоединять не только списки, но и любой iterable. Помещение его внутрь строки предотвращает реализацию одной и той же функциональности в нескольких местах.

## 21. Query JSON

JMESpath – это язык запросов для JSON, который позволяет получать необходимые данные из документа или словаря JSON. Библиотека доступна как для Python, так и для других ЯП, что расширяет ее возможности.

Вот несколько примеров кода для общего представления:

``` py
>>> import jmespath
>>> persons = {
...   "persons": [
... { "name": "erik", "age": 38 },
... { "name": "john", "age": 45 },
... { "name": "rob", "age": 14 }
...   ]
... }
>>> jmespath.search('persons[*].age', persons)
[38, 45, 14]
```

## 22. Реверс строк и списков

Вы можете использовать slice\-нотацию, чтобы перевернуть строку или список. При отрицательном значении шага, элементы меняются местами:

``` py
revstring = "abcdefg"[::-1]
print(revstring)
# 'gfedcba'

revarray = [1, 2, 3, 4, 5][::-1]
print(revarray)
# [5, 4, 3, 2, 1]
```

## 23. Получение уникальных элементов из списка или строки

Создавая набор с помощью функции **set()**, вы получаете все уникальные элементы из списка или объекта:

``` py
mylist = [1, 1, 2, 3, 4, 5, 5, 5, 6, 6]
print (set(mylist))
# {1, 2, 3, 4, 5, 6}

# And since a string can be treated like a 
# list of letters, you can also get the 
# unique letters from a string this way:
print (set("aaabbbcccdddeeefff"))
# {'a', 'b', 'c', 'd', 'e', 'f'}
```

## 24. Валидные значения словаря

В словарь можно поместить что угодно – вы не ограничены числами или строками. Можете поместить списки внутрь словаря и получить доступ к вложенным значениям:

``` py
>>> a = { 'sub_dict': { 'b': True }, 'mylist': [100, 200, 300] }
>>> a['sub_dict']['b']
True
>>> a['mylist'][0]
100
```

## 25. Тернарный оператор условного присваивания

Это еще один способ сделать код более кратким и сохранить его читабельность:

``` py
[on_true] if [expression] else [on_false]
```

А вот пример:

``` py
x = "Success!" if (y == 2) else "Failed!"
```

## 26. Подсчет вхождений в список

Используйте **Counter** из библиотеки коллекций, чтобы получить словарь с подсчетом всех уникальных элементов в списке:

``` py
from collections import Counter

mylist = [1, 1, 2, 3, 4, 5, 5, 5, 6, 6]
c = Counter(mylist)
print(c)
# Counter({1: 2, 2: 1, 3: 1, 4: 1, 5: 3, 6: 2})

# And it works on strings too:
print(Counter("aaaaabbbbbccccc"))
# Counter({'a': 5, 'b': 5, 'c': 5})
```

## 27. Цепочки операторов сравнения

Создавайте еще более читаемый и аккуратный код:

``` py
x = 10

# Instead of:
if x > 5 and x < 15:
print("Yes")
# yes

# You can also write:
if 5 < x < 15:
print("Yes")
# Yes
```

## 28. Работа с датами

![](https://media.proglib.io/posts/2021/02/13/08254d37f827f5bfe9f616bfcbdd104f.jpg)

Модуль [python-dateutil](https://pypi.org/project/python-dateutil/) предоставляет мощное расширение для стандартного datetime. Устанавливается он следующим образом:

``` bash
pip3 install python-dateutil
```

Вот пример парсинга даты из логов:

``` py
from dateutil.parser import parse

logline = 'INFO 2020-01-01T00:00:01 Happy new year, human.'
timestamp = parse(logline, fuzzy=True)
print(timestamp)
# 2020-01-01 00:00:01
```

## 29. Использование map()

Такой синтаксис имеет данная встроенная функция:

``` py
map(function, something_iterable)
```

Ниже видите пример с использованием списков:

``` py
def upper(s):
return s.upper()

mylist = list(map(upper, ['sentence', 'fragment']))
print(mylist)
# ['SENTENCE', 'FRAGMENT']

# Convert a string representation of
# a number into a list of ints.
list_of_ints = list(map(int, "1234567"))
print(list_of_ints)
# [1, 2, 3, 4, 5, 6, 7]
```

## 30. Словарь и set comprehensions

Словарю нужны ключ и значение:

``` py
>>> {x: x**2 for x in (2, 4, 6)}
{2: 4, 4: 16, 6: 36}
```

Определяем ключ и значение в expression.

Синтаксис set comprehension не сильно отличается от list comprehension. Мы просто используем фигурные скобки вместо квадратных:

``` py
{ <expression> for item in list if <conditional> }
```

Пример:

``` py
>>> {s for s in range(1,5) if s % 2}
{1, 3}
```

## Заключение

В современном динамичном мире важно знать как можно больше хитростей, ускоряющих рутинную работу разработчика. Рассмотренная подборка отвечает всем требованиям повышенного уровня сложности и при должном количестве потраченного времени сможет вырастить из вас профессионала – главное не сдавайтесь! Удачи!

Дополнительный материал:

* [Микросервисная архитектура на примере Python и gRPC](https://proglib.io/p/mikroservisnaya-arhitektura-na-primere-python-i-grpc-2021-02-12)
* [Хватит использовать print для отладки в Python: переходите на Icecream](https://proglib.io/p/hvatit-ispolzovat-print-dlya-otladki-v-python-perehodite-na-icecream-2021-01-20)

* [Туториал: визуализация данных в вебе с помощью Python и Dash](https://proglib.io/p/tutorial-vizualizaciya-dannyh-v-vebe-s-pomoshchyu-python-i-dash-2021-01-11)

* [Самоучитель для начинающих: как освоить Python с нуля за 30 минут?](https://proglib.io/p/bystryy-samouchitel-kak-osvoit-python-za-30-minut-2021-01-11)

* [Топ-20 бесплатных ресурсов для изучения Python: сохрани это в закладки](https://proglib.io/p/top-20-besplatnyh-resursov-dlya-izucheniya-python-sohrani-eto-v-zakladki-2021-01-08)

## Источник

* [https://medium.com/pythonland/30-python-language-tricks-that-will-make-you-a-better-coder-f08f811a7b0f](https://medium.com/pythonland/30-python-language-tricks-that-will-make-you-a-better-coder-f08f811a7b0f)

## Ссылки на эту страницу

* [Python](Python.md)
