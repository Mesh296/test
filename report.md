# НАЦИОНАЛЬНЫЙ ИССЛЕДОВАТЕЛЬСКИЙ УНИВЕРСИТЕТ ИНФОРМАЦИОННЫХ ТЕХНОЛОГИЙ, МЕХАНИКИ И ОПТИКИ
 
### Факультет инфокоммуникационных технологий
### **Дисциплина “Алгоритмы и структуры данных”**
### *Отчет к лабораторной работе второго семестра № 1*
**Выполнил:**  студент группы К3139 - Чан Дык Минь
 
**Принял:** преподаватель Татьяна Александровна Харьковская
 
*Санкт-Петербург*
*2021 год*

___

**Задание 1: В упражнении нам предлагается найти максимальное значение, которое можно положить в карман.**

Сначала делим каждый объект на сколько значений 1g. Затем отсортируйте значение в порядке от большего к меньшему. Далее мы берем каждый предмет до тех пор, пока сумка больше не сможет его удерживать.

```python
f = open("input.txt", "r")
n, w = map(float, f.readline().split())
stuffs = {}
bag = 0
for i in range(int(n)):
    x, y = map(float, f.readline().split())
    if x/y not in stuffs:
        stuffs[x/y] = y
    else:
        stuffs[x/y] += y
f.close()
stuffs = sorted(stuffs.items(), reverse=True)
for st in stuffs:
    if w >= st[1]:
        bag += st[0] * st[1]
        w -= st[1]
    elif w < st[1]:
        bag += st[0] * w
        break
f = open("output.txt", "w")
f.write(str(format(bag, '.4f')))
f.close()
```
**Задание 2: В этом упражнении нам предлагается найти способ останавливаться на как можно меньшем количестве заправок.**

Найдите максимальную остановку, которую может проехать автомобиль. Затем остановитесь там и продолжайте искать следующую станцию. Каждый раз увеличивайте переменную "res" на 1 (переменная результата).Если следующая остановка не может быть достигнута, выведите -1.

```python
f = open("input.txt", "r")
d = int(f.readline())
m = int(f.readline())
n = int(f.readline())
station = list(map(int, f.readline().split()))
station.append(d)
f.close()
res = 0
stop = 0
def find():
    global res, stop
    for i in range(n): #tim trạm tối đa xe tới đc
        if station[i] <= stop + m and station[i+1] > stop + m:
            stop = station[i]
            res += 1
        if station[i] > stop + m:
            res = -1
            break
    return str(res)
f = open("output.txt", "w")
if m >= d: f.write("0")
else: f.write(find())
f.close()
```

**Задание 3: Найдите способ разместить рекламные щиты, чтобы максимизировать продажи**

Мы переставляем два массива «а» (массив доходов) и массив «б» (количество кликов в день). тогда мы получим меньше кликов, что соответствует меньшему доходу, и наоборот. Далее вычисляем общую выручку и получаем результат.

```python
f = open("input.txt", "r")
n = int(f.readline())
a = list(map(int, f.readline().split()))
b = list(map(int, f.readline().split()))
f.close()
a = sorted(a)
b = sorted(b) 
res = 0
for i in range(n): 
    res += a[i]*b[i]
f = open("output.txt", "w")
f.write(str(res))
f.close()
```

 
**Задание 4: Найдите минимальное множество целых чисел E, такое что каждый сегмент имеет атрибут E**

Сначала мы переставляем массив в порядке позиции x. Назовем общее число «i» первой y-позицией. Затем мы просматриваем массив сверху вниз и находим общее число, которое является наибольшим числом меньше y и наименьшим числом больше x. Если «i» больше x, добавьте i в массив res и начните новый i.

```python
def Read():
    global n, a
    a = []
    f = open("input.txt", "r")
    n = int(f.readline())
    for i in range(n):
        x, y = map(int, f.readline().split())
        a.append([x, y])
def find():
    global a, res, cnt
    res = []
    a = sorted(a)
    i = a[0][1] 
    cnt = 1
    for x, y in a:
        if x <= i:
            i = min(y, i)
        if x > i:
            res.append(i)
            cnt += 1
            i = y
    res.append(i)
def Write():
    f = open("output.txt", "w")
    f.write(str(cnt) + '\n')
    for i in res:
        f.write(str(i)+" ")
Read()
find()
Write()
```

**Задание 5: Find a way to represent a number into as many numbers as possible so that their sum is equal to that number**

у нас есть первая i-значная формула, которую можно представить как сумму не более чем i-1 чисел. Итак, мы просто выводим i-2 числа, и последнее число равно n минус сумма i-2 чисел.

```python
f = open("input.txt", "r")
n = int(f.readline())
cnt = 1 
Sum = 0 
f.close()
while Sum < n: 
    cnt += 1 
    Sum += cnt
f = open("output.txt", "w")
for i in range(1, cnt-1):
    f.write(str(i) + " ")
    n -= i
f.write(str(n))
f.close()
```

**Задание 6: Отсортируйте данные числа по наибольшему числу.**

Мы делаем то же самое, что и алгоритм пузырьковой сортировки, запускаем циклы 2 for и сравниваем, меньше ли порядок числа перед следующим числом, чем порядок числа после предыдущего числа, а затем меняем местами эти два числа.

```python
f = open("input.txt", "r")
n = int(f.readline())
a = list(map(str, f.readline().split()))
f.close()
for i in range(0,n-1):
    for j in range(i+1,n):
        if a[i] + a[j] < a[j] + a[i]:
            a[i], a[j] = a[j], a[i]
f = open("output.txt", "w")
for i in a:
    f.write(i)
f.close()
```

**Задание 7: Найдите максимальное количество обуви, изготовленной за 1 день.**

Мы располагаем время завершения каждой обуви в порядке от меньшего к большему, затем просматриваем от начала до конца, если время для завершения i-й обуви меньше, чем оставшееся время в этот день, мы вычитаем время для завершения i-й обуви и увеличиваем переменная "res" (результат) на 1.

```python
f = open("input.txt", "r")
time, n = map(int, f.readline().split())
a = list(map(int, f.readline().split()))
res = 0
f.close()
a = sorted(a)
for i in a:
    if time > i:
        time -= i
        res += 1
    else: break
f = open("output.txt", "w")
f.write(str(res))
f.close()
```
**Задание 8: Найдите максимальное количество лекций.**

Сначала мы отмечаем время лекции. Затем просмотрите и узнайте, был ли урок, который закончился раньше, прибавляем переменную res (результат) на 1.

```python
cld = {}
begin = 0
end = 0
res = 1
f = open("input.txt", "r")
n = int(f.readline())
for _ in range(n):
    x, y = map(int, f.readline().split())
    cld[x] = y
    begin, end = max(x, begin), max(y, end)
dp = [[0 for _ in range(end+1)] for _ in range(begin+1)]
for i in range(1, begin+1):
    for j in range(1, end+1):
        if i in cld and (cld[i] > j and j >= i):
            dp[i][j] = 1
for i in range(1, begin+1):
    for j in range(1, end+1):
        if dp[i-1][j-1] and dp[i][j] and not dp[i-1][j]:
            dp[i][j] += dp[i-1][j-1]
            res = max(res, dp[i][j])
print(res)
```
**Задание 10: Найдите порядок поедания яблок, чтобы высота не уменьшилась до 0.**

Мы делим количество яблок на два массива, первый массив содержит количество яблок, которые больше увеличивают высоту, а другой массив содержит количество яблок, которые больше уменьшают высоту. Мы сортируем эти два массива в порядке возрастания убывания. Сначала мы съедаем по очереди все яблоки из массива один, затем по очереди съедаем все яблоки из массива два. Если есть случай, когда высота падает до нуля, яблоко съесть невозможно.

```python

up, down = [], []
f = open("input.txt", "r")
n, s = map(int, f.readline().split())
for i in range(n):
    x, y = map(int, f.readline().split())
    if x <= y: up.append([x, y, i+1])
    else: down.append([x, y, i+1])
f.close()
up = sorted(up)
down = sorted(down)
for _ in up:
    if s >= _[0]:
        s -= _[0]
        s += _[1]
    else:
        s = -1
        break
if s != -1:
    for _ in down:
        if s >= _[0]:
            s -= _[0]
            s += _[1]
        else:
            s = -1
            break
f = open("output.txt", "w")
if s != -1:
    for _ in up:
        f.write(str(_[2]) + " ")
    for _ in down:
        f.write(str(_[2]) + " ")
else: f.write("-1")
```

**Задание 11: Найдите максимальную полученную стоимость золота.**

считаем при значении j, если j больше i-го объекта, то берем золотое значение при j по формуле (dp[i][j] = max(dp[i-1][j], dp[i-1][j-w[i]] + w[i]))

```python
f = open("input.txt", "r")
weight, n = map(int, f.readline().split())
dp = [[0 for i in range(weight + 1)] for i in range(n + 1)]
w = list(map(int, ("0 " + f.readline()).split()))
f.close()
for i in range(1, n + 1):
    for j in range(1, weight + 1):
        dp[i][j] = dp[i-1][j]
        if j >= w[i]:  
            dp[i][j] = max(dp[i-1][j], dp[i-1][j-w[i]] + w[i]) 

f = open("output.txt", "w")
f.write(str(dp[n][weight]))
f.close()
```
**Задание 13: 3 подпоследовательности с одинаковой суммой**

Пусть сумма, которую каждая из трех подпоследовательностей образует s (s = SUM/3). Мы используем рекурсию, чтобы найти числа с суммой = s и снова отметить, продолжаем использовать рекурсию, чтобы найти оставшиеся 2 массива. Если вы найдете 3 массива с одинаковыми суммами, выведите 1, иначе выведите 0.

```python
def Read():
    global arr, mark, n, target
    f = open("input.txt", "r")
    n = int(f.readline())
    mark = [0] * n
    arr = list(map(int, f.readline().split()))
    target = sum(arr) // 3
    f.close()
def recursion(x, start):
    global check
    if x == target:
        check = True
    for i in range(start, n):
        if x + arr[i] <= target and mark[i] == 0:
            x += arr[i]
            mark[i]=1
            recursion(x, i+1)
            x -= arr[i]
            mark[i]=0
def solve():
    global check
    for i in range(3):
        check = False
        recursion(0, 0)
    if check == True: return 1
    else: return 0
Read()
f = open("output.txt", "w")
f.write(str(solve()))
f.close()
```

**Задание 17: Найдите телефонные номера, которые можно сгенерировать, перемещая коня.**

Создайте список «nb», то есть список смежности числа i с последующими номерами. Мы проходим через цикл while, чтобы найти из числа, начиная с i (0 < i < 10, i!= 8), сколько чисел длины «cnt» можно сгенерировать, затем накапливаем и сохраняем в «prior_Case» и находим следующее экземпляр с длиной "cnt+1". Наконец, мы складываем 8 случаев.

```python
f = open("input.txt", "r")
n = int(f.readline())
f.close()
nb = { 
    1: (6, 8),
    2: (7, 9),
    3: (4, 8),
    4: (3, 9, 0),
    5: tuple(),
    6: (1, 7, 0),
    7: (2, 6),
    8: (1, 3),
    9: (2, 4),
    0: (4, 6),
}
def count_sequences(start, length):
    if length == 0: return 8
    prior_case = [1] * 10 
    current_case = [0] * 10
    cnt = 1
    while cnt <= length:
        current_case = [0] * 10
        cnt += 1
        for pos in range(0, 10):
            for neighbor in nb[pos]:
                current_case[pos] += prior_case[neighbor]
        print(current_case)
        prior_case = current_case
    res = 0
    for i in range(0,10):
        if not i in [0, 8]: res += current_case[i]
    return res%(10**9)
f = open("output.txt", "w")
f.write(str(count_sequences(0, n-1)))
f.close()
```

**Задание 18: Найдите минимальную сумму, подлежащую выплате через n дней. **

We will use the array (dp[i][j][k] to store the minimum amount of money spent for lunch after i days, there are j coupons and k coupons used. We will divide it into three fields. combine and use the corresponding dynamic programming formula:
  
  - if (a[i] < 100): dp[i][j][k] = dp[i-1][j][k] + a[i]
  - if (a[i] >= 100): dp[i][j+1][k] = dp[i-1][j][k] + a[i]
  - if (dp[i][j][k] > dp[i - 1][j][k - 1]): dp[i][j][k] = dp[i - 1][j][k - 1]

After all, we have "res" is the amount of money, that is the maximum value in dp and array "save" is the day we use coupon.

```python
f = open("input.txt", "r")
n = int(f.readline())
a = [0] * (n+1)
for i in range(1, n+1):
    a[i] = int(f.readline())
dp = [[[(10**9) for k in range(n + 1)] for j in range(n + 1)] for i in range(n + 1)]
recur = [[[(0) for k in range(n + 1)] for j in range(n + 1)] for i in range(n + 1)]
dp[0][0][0] = 0
for i in range(1, n + 1):
    for j in range(0, i + 1):
        for k in range(0, j + 1):
            if (a[i] < 100): 
                if (dp[i][j][k] > dp[i - 1][j][k] + a[i]): 
                    recur[i][j][k] = (j, k) 
                    dp[i][j][k] = dp[i - 1][j][k] + a[i]
            if (a[i] >= 100 and j < n): 
                if (dp[i][j + 1][k] > dp[i - 1][j][k] + a[i]):
                    dp[i][j + 1][k] = dp[i - 1][j][k] + a[i]
                    recur[i][j + 1][k] = (j, k)
            if (dp[i][j][k] > dp[i - 1][j][k - 1]):
                dp[i][j][k] = dp[i - 1][j][k - 1]
                recur[i][j][k] = (j, k - 1)
res = 10 ** 9
X, Y, Z = n, 0, 0
for j in range(0, n + 1):
    for k in range(0, n + 1):
        if (res > dp[n][j][k]):
            res = dp[n][j][k]
            Y = j
            Z = k
f = open("output.txt", "w")
f.write(str(res) + "\n")
f.write(str(Y - Z) + " " + str(Z) + "\n")
save = []
while (recur[X][Y][Z]):
    if (recur[X][Y][Z] == (Y, Z - 1)):
        save.append(X)
    Y, Z = recur[X][Y][Z]
    X -= 1
save.reverse()
for i in save:
    f.write(str(i) + "\n")
```

**Вывод:** я научился использовать жадный алгоритм и алгоритм динамического программирования.