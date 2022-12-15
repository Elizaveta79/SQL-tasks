+ [1](#1)
+ [2](#2)
+ [3](#3)
+ [4](#4)
+ [5](#5)
+ [6](#6)
+ [7](#7)
+ [8](#8)
+ [9](#9)
+ [10](#10)
+ [11](#11)
+ [12](#12)
+ [13](#13)
+ [14](#14)
+ [15](#15)
+ [16](#16)
+ [17](#17)
+ [18](#18)
+ [19](#19)
+ [20](#20)

## 1

https://sql-ex.ru/learn_exercises.php?LN=1

Найдите номер модели, скорость и размер жесткого диска для всех ПК стоимостью менее 500 дол. Вывести: model, speed и hd

```sql
SELECT model, speed, hd
FROM PC
WHERE price < 500
```

## 2

https://sql-ex.ru/learn_exercises.php?LN=2

Найдите производителей принтеров. Вывести: maker

```sql
SELECT DISTINCT maker FROM Product
WHERE Product.type = 'Printer'
```

## 3

https://sql-ex.ru/learn_exercises.php?LN=3

Найдите номер модели, объем памяти и размеры экранов ПК-блокнотов, цена которых превышает 1000 дол.

```sql
SELECT model, ram, screen
FROM Laptop
WHERE price > 1000
```

## 4

https://sql-ex.ru/learn_exercises.php?LN=4

Найдите все записи таблицы Printer для цветных принтеров.

```sql
SELECT * FROM Printer
WHERE color = 'y'
```

## 5

https://sql-ex.ru/learn_exercises.php?LN=5

Найдите номер модели, скорость и размер жесткого диска ПК, имеющих 12x или 24x CD и цену менее 600 дол.

```sql
SELECT model, speed, hd FROM PC
WHERE (cd ='12x' or cd = '24x') and price < 600
```

## 6

https://sql-ex.ru/learn_exercises.php?LN=6

Для каждого производителя, выпускающего ПК-блокноты c объёмом жесткого диска не менее 10 Гбайт, найти скорости таких ПК-блокнотов. Вывод: производитель, скорость.

```sql
SELECT DISTINCT maker, speed FROM Product INNER JOIN Laptop
ON Product.model = Laptop.model
WHERE hd >=10
```

## 7

https://sql-ex.ru/learn_exercises.php?LN=7

Найдите номера моделей и цены всех имеющихся в продаже продуктов (любого типа) производителя B (латинская буква).

```sql
SELECT Laptop.model, Laptop.price FROM Laptop INNER JOIN Product ON Laptop.model = Product.model  
WHERE Product.maker = 'B' 
UNION 
SELECT PC.model, PC.price FROM PC INNER JOIN Product ON PC.model = Product.model  
WHERE Product.maker = 'B' 
UNION
SELECT Printer.model, Printer.price FROM Printer INNER JOIN Product ON Printer.model = Product.model  
WHERE Product.maker= 'B'
```

## 8

https://sql-ex.ru/learn_exercises.php?LN=8

Найдите производителя, выпускающего ПК, но не ПК-блокноты.

```sql
SELECT maker FROM Product WHERE type = 'PC'
EXCEPT
SELECT maker FROM product WHERE type = 'laptop'
```

## 9

https://sql-ex.ru/learn_exercises.php?LN=9

Найдите производителей ПК с процессором не менее 450 Мгц. Вывести: Maker

```sql
SELECT DISTINCT maker FROM Product
INNER JOIN PC ON pc.model = product.model
WHERE pc.speed >= 450
```

## 10

https://sql-ex.ru/learn_exercises.php?LN=10

Найдите модели принтеров, имеющих самую высокую цену. Вывести: model, price

```sql
SELECT DISTINCT model, price 
FROM Printer 
WHERE price = (SELECT MAX(price) FROM Printer)
```

## 11

https://sql-ex.ru/learn_exercises.php?LN=11

Найдите среднюю скорость ПК.

```sql
SELECT AVG(speed) FROM PC
```

## 12

https://sql-ex.ru/learn_exercises.php?LN=12

Найдите среднюю скорость ПК-блокнотов, цена которых превышает 1000 дол.

```sql
SELECT AVG(speed) 
FROM Laptop 
WHERE price > 1000
```

## 13

https://sql-ex.ru/learn_exercises.php?LN=13

Найдите среднюю скорость ПК, выпущенных производителем A.

```sql
SELECT AVG(speed) 
FROM PC 
JOIN product ON pc.model = product.model 
WHERE maker = 'A'
```

## 14

https://sql-ex.ru/learn_exercises.php?LN=14

Найдите класс, имя и страну для кораблей из таблицы Ships, имеющих не менее 10 орудий.

```sql
SELECT Ships.class, Ships.name, Classes.country
FROM Ships
JOIN classes ON Ships.class = Classes.class
WHERE numGuns >= 10
```

## 15

https://sql-ex.ru/learn_exercises.php?LN=15

Найдите размеры жестких дисков, совпадающих у двух и более PC. Вывести: HD

```sql
SELECT hd 
FROM PC 
GROUP BY hd 
HAVING COUNT(hd) >= 2
```

## 16

https://sql-ex.ru/learn_exercises.php?LN=16

Найдите пары моделей PC, имеющих одинаковые скорость и RAM. В результате каждая пара указывается только один раз, т.е. (i,j), но не (j,i), Порядок вывода: модель с большим номером, модель с меньшим номером, скорость и RAM.

```sql
SELECT DISTINCT pc1.model, pc2.model, pc1.speed, pc1.ram
FROM PC AS pc1, PC AS pc2
WHERE pc1.speed = pc2.speed AND pc1.ram = pc2.ram AND pc1.model > pc2.model
```

## 17

https://sql-ex.ru/learn_exercises.php?LN=17

Найдите модели ПК-блокнотов, скорость которых меньше скорости каждого из ПК.
Вывести: type, model, speed

```sql
SELECT DISTINCT Product.type, Laptop.model, Laptop.speed From Laptop
JOIN Product ON Laptop.model=Product.model
WHERE Laptop.speed < (SELECT MIN(speed) FROM PC)
```

## 18

https://sql-ex.ru/learn_exercises.php?LN=18

Найдите производителей самых дешевых цветных принтеров. Вывести: maker, price

```sql
SELECT DISTINCT Product.maker, Printer.price FROM Product, Printer
WHERE Product.model = Printer.model AND Printer.color = 'y' AND Printer.price = (SELECT MIN(price) FROM Printer WHERE color = 'y')
```

## 19

https://sql-ex.ru/learn_exercises.php?LN=19

Для каждого производителя, имеющего модели в таблице Laptop, найдите средний размер экрана выпускаемых им ПК-блокнотов.
Вывести: maker, средний размер экрана.

```sql
SELECT Product.maker, AVG(screen)
FROM Laptop
JOIN Product ON Product.model = Laptop.model
GROUP BY Product.maker
```

## 20

https://sql-ex.ru/learn_exercises.php?LN=20

Найдите производителей, выпускающих по меньшей мере три различных модели ПК. Вывести: Maker, число моделей ПК.

```sql
SELECT maker, COUNT(model) FROM Product WHERE type = 'PC'
GROUP BY Product.maker
HAVING COUNT (DISTINCT model) >= 3
```
