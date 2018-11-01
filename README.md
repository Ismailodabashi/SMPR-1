# SMPR
Language R


  - [Метрические алгоритмы классификации](#Метрические-алгоритмы-классификации)
  - [1NN](#1NN)
  - [KNN](#KNN)
  - [KWNN](#KWNN)
 
  
## Метрические алгоритмы классификации

**Метрические методы обучения** -- методы, основанные на анализе сходства объектов.

Метрические алгоритмы классификации опираются на **_гипотезу компактности_**: схожим объектам соответствуют схожие ответы.

Метрические алгоритмы классификации с обучающей выборкой *Xl* относят объект *u* к тому классу *y*, для которого **суммарный вес ближайших обучающих объектов ![](https://latex.codecogs.com/gif.latex?W_y%28u%2C%20X%5El%29) максимален**:

![](https://latex.codecogs.com/gif.latex?W_y%28u%2C%20X%5El%29%20%3D%20%5Csum_%7Bi%20%3A%20y_%7Bu%7D%5E%7B%28i%29%7D%20%3D%20y%7D%20w%28i%2C%20u%29%20%5Crightarrow%20max)

, где весовая функция *w(i, u)* оценивает степень важности *i*-го соседа для классификации объекта *u*.

Функция ![](https://latex.codecogs.com/gif.latex?W_y%28u%2C%20X%5El%29) называется **_оценкой близости объекта u к классу y_**. Выбирая различную весовую функцию *w(i, u)* можно получать различные метрические классификаторы.

### Методы ближайших соседей

Классификация ирисов Фишера методом 1NN (ближайшего соседа)

Решалась задача классификации. В качестве обучающей выборки была взята матрица ирисов фишера по длине и ширине лепестка.
Требовалось построить карту классификации на основе данных обучающей выборки.
В качестве метода классификации использовался метод 1NN.
## 1NN 
# Метод 1NN состоит в следующем: 
	1.Для классифицируемого объекта вычисляются расстояния от него до каждого объекта обучающей выборки.
	2.Обучающая выборка сортируется по возрастанию расстояния от каждого объекта выборки до классифицируемого
	3.Классифицируемому объекту присваивается тот же класс, что и ближайшего к нему объекта выборки.
 
 
  <p><img src="img\1nn.png" ></p>
  
Классификация ирисов Фишера методом kNN (k ближайших соседей)


Решалась задача классификации. В качестве обучающей выборки была взята матрица ирисов фишера по длине и ширине лепестка.
Требовалось построить карту классификации на основе данных обучающей выборки.
В качестве метода классификации использовался метод kNN.


  ## KNN 


 Метод kNN состоит в следующем: 
	1.Для классифицируемого объекта вычисляются расстояния от него до каждого объекта обучающей выборки
	2.Обучающая выборка сортируется по возрастанию расстояния от каждого объекта выборки до классифицируемого
	3.Подсчитывается, какой класс доминирует среди k ближайших соседей, и этот класс присваивается классифицируемому объекту
	## Алгоритм k ближайших соседей (kNN)
Алгоритм 1NN относит классифицируемый объект U к тому классу, которому принадлежит его ближайший сосед.
ὠ(i,u)=[i=1];

Алгоритм kNN относит объект к тому классу, элементов которого больше среди k ближайших соседей x(i), i=1,..,k.

Для оценки близости классифицируемого объекта *u* к классу *y* **алгоритм kNN** использует следующую функцию:

ὠ(i,u)=[i<=k], где *i* -- порядок соседа по расстоянию к классифицируемому объекту *u*, k-количество параметровю=.
**Реализация весовой функции производится следующим образом**:

``` R
distances <- matrix(NA, l, 2) # расстояния от классифицируемого объекта u до каждого i-го соседа 
for(i in 1:l) {
   distances[i, ] <- c(i, eDist(xl[i, 1:n], u))
}
orderedxl <- xl[order(distances[ , 2]), ] # сортировка расстояний
classes <- orderedxl[1:k, n + 1] # названия первых k классов (k ближайших соседей) в classes 
```

<p><img src="img\LooKnn.png" ></p>

### Преимущества:
1. Простота реализации.
2. При *k*, подобранном около оптимального, алгоритм "неплохо" классифицирует.

### Недостатки:
1. Нужно хранить всю выборку.
2. При *k = 1* неустойчивость к погрешностям (*выбросам* -- объектам, которые окружены объектами чужого класса), вследствие чего этот выброс классифицировался неверно и окружающие его объекты, для которого он окажется ближайшим, тоже.
2. При *k = l* алгоритм наоборот чрезмерно устойчив и вырождается в константу.
3. Крайне бедный набор параметров.
4. Точки, расстояние между которыми одинаково, не все будут учитываться.

## KWNN
Реализаця метода kwNN
В каждом классе выбирается
__k__ ближайших к __U__ объектов, и объект u относится к тому классу, для
которого среднее расстояние до __k__ ближайших соседей минимально.
![](http://latex.codecogs.com/gif.latex?w%28i%2Cu%29%3D%5Bi%5Cleq%20k%5Dw%28i%29)
где,
![](http://latex.codecogs.com/gif.latex?w%28i%29) — строго убывающая последовательность вещественных весов, задающая
вклад i-го соседа при классификации объекта u.

<p><img src="img\LooKwnn.png" ></p>

kNN — один из простейших алгоритмов классификации, поэтому на реальных задачах он зачастую оказывается неэффективным. Помимо точности классификации, проблемой этого классификатора является скорость классификации: если в обучающей выборке N объектов, в тестовой выборе M объектов, а размерность пространства — K, то количество операций для классификации тестовой выборки может быть оценено как O(KMN).

kwNN отличается от kNN, тем что учитывает порядок соседей классифицируемого объекта, улчшая качество классификации.
	
Число k выбирается методом LOO (скользящего контроля)


### Метод LOO:
1. Элемент удаляется из выборки
2. Запускается алгоритм классификации (в данном случае kNN) для полученной выборки и удалённого объекта
3. Полученный класс объекта сравнивается с реальным. В случае несовпадения классов, величина ошибки увеличивается на 1
4. Процесс повторяется для каждого объекта выборки
5. Полученная ошибка усредняется
6. Процесс повторяется для других значений k. В итоге выбирается число k с наименьшей ошибкой LOO
    

```	
##Составляем таблицу встречаемости каждого класса
counts <- table(classes)
class <- names(which.max(counts))
return (class)
}

## Метод скользящего контроля
Loo <- function(k,xl)
   {
    sum =0
    for(i in 1:dim(xl)[1]
       {
        tmpXL <- rbind(xl[1:i-1, ],
        xl[i+1:dim(xl)[1],])
        xi <- c(xl[i,1], xl[i,2])
        class <-kNN(tmpXL,xi,k)
        if(class != xl[i,3])
        sum=sum+1
       }
   sum=sum/dim(xl)[1]
   return(sum)
  }
```

 ### Преимущества:
 Преимущество LOO состоит в том, что каждый объект ровно один раз участвует в контроле, а длина обучающих подвыборок лишь на единицу меньше длины полной выборки.
 ### Недостатки:
  Недостатком LOO является большая ресурсоёмкость, так как обучаться приходится L раз. Некоторые методы обучения позволяют достаточно быстро перенастраивать внутренние параметры алгоритма при замене одного обучающего объекта другим. В этих случаях вычисление LOO удаётся заметно ускорить. 
  
  <center>
<table>
  <tbody>
    <tr>
      <th>Метод</th>
      <th>Параметры</th>
      <th>Точность</th>
    </tr>
    <tr>
      <td>KWNN</a></td>
      <td>k=9</td>
      <td>0.0333</td>
    </tr>
    <tr>
      <td>KNN</a></td>
      <td>k=6</td>
      <td>0.0333</td>
    </tr>
	  </tbody>
   </table>

#### Сравнение качества алгоритмов kNN и kwNN.

kNN — один из простейших алгоритмов классификации, поэтому на реальных задачах он зачастую оказывается неэффективным. Помимо точности классификации, проблемой этого классификатора является скорость классификации: если в обучающей выборке N объектов, в тестовой выборе M объектов, а размерность пространства — K, то количество операций для классификации тестовой выборки может быть оценено как O(KMN).

kwNN отличается от kNN, тем что учитывает порядок соседей классифицируемого объекта, улчшая качество классификации.
