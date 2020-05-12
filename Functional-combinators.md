# Functional Combinators

**`List(1, 2, 3) map squared`对列表中的每一个元素都应用了`squared`平方函数，并返回一个新的列表`List(1, 4, 9)`。我们把类似于`map`的操作称作*组合子*。 （如果想要更好的定义，你可以看看Stackoverflow上对[组合子的说明](http://stackoverflow.com/questions/7533837/explanation-of-combinators-for-the-working-man)。）他们常被用在标准的数据结构上。** 

组合子（combinator），是函数式编程里面的重要思想。组合子通过定义最基本的原子操作，定义基本的组合规则，然后把这些原则以各种方法组合起来。也有人把面向组合子（Combinator-Oriented）的编程思想叫做“演绎法”，相对于分析归纳需求并根据需求高度抽象为对象且面向于对象的编程思想（OO，Object Oriented也有人叫归纳法）而言，组合子更具有函数式的思想。

OO思想（归纳法）怎么理解呢？其实OO是我们最常见的一种编程思路，往往是由需求导向，先有了需求，然后我们根据需求分析问题，进行拆分，最后抽象为对象然后转化为我们的程序语言逻辑实现。

CO思想怎么理解呢？CO更像是搭积木，我们有各种积木（即组合子），根据积木的各种组合从而获得形式各异的造型结构。

总之一句话。OO的原材料（对象）需要我们自己构建，CO提供了原材料（组合子）库供我们自己选择使用。

## map

map方法可以将某个函数应用到集合中的每个元素并产出其结果的集合。举例：

```scala
val names = List("a","b","c")
names.map(_.toUpperCase)
```

得到结果

```scala
List("A","B","C")
```

注意map使用时关键需要知道其中每一项的内容和格式，注意下面中map配合解析的情况。



```scala
val scid = Seq("39612569::0:2728:0:1,32100650::0:2730:0:2,32218352::0:2730:0:3,32042828::0:2730:0:4,105894131::0:2730:0:5,32144418::0:2728:0:6,40288371::0:2728:0:7", "32029511::0:2730:0:8,32218351::0:2728:0:9", "32029500::0:2730:0:8,32029511::0:2728:0:8")

scid.map(_.split(",")). //生成list of array，即 Seq[Array[String]]
flatten. //将List中的Array进行展开
map(_.split(":")).
map((i:Array[String]) => (i(5), i(0))). //将Seq[Array[String]]变成Seq[(String, String)]
groupBy(_._1).
values.
map((i:Seq[(String, String)]) => i.groupBy(identity).mapValues{_.length}.maxBy(_._2)._1).
map((i:(String, String))  => Map(i._1.toInt -> i._2)).
reduce(_ ++ _) //将list of map变成一个map
```

如果遇到复杂的，则采用**case需要搭配花括号**：

```scala
val m1 = Map((3,5) -> "geeks", (4,6) -> "for", (4,7) -> "for")
m1.toList.map{case (i, s) => (i._1, i._2, s)}
```

另外对于将Map转换为tuple，实际上map已经是tuple了。**所以可以直接像上面一样使用toList，然后再根据要求调整顺序。**

```scala
scala> "b" -> 2
res0: (String, Int) = (b,2) // Implicitly converted to a Tuple
```



##flatmap（常用于嵌套list中）

flatMap is a frequently used combinator that combines mapping and flattening. flatMap takes a function that works **on the nested lists and then concatenates the results back together.**

```
scala> val nestedNumbers = List(List(1, 2), List(3, 4))
nestedNumbers: List[List[Int]] = List(List(1, 2), List(3, 4))

scala> nestedNumbers.flatMap(x => x.map(_ * 2))
res0: List[Int] = List(2, 4, 6, 8)
```

**Think of it as short-hand for mapping and then flattening:**

```
scala> nestedNumbers.map((x: List[Int]) => x.map(_ * 2)).flatten
res1: List[Int] = List(2, 4, 6, 8)
```

that example calling map and then flatten is an example of the “combinator”-like nature of these functions.

## zip

`zip`将两个列表的内容聚合到一个对偶列表中。

```
scala> List(1, 2, 3).zip(List("a", "b", "c"))
res0: List[(Int, String)] = List((1,a), (2,b), (3,c))
```

## zipWithIndex

返回序号，从0开始，将结果返回形式为`Array((Sunday,0), (Monday,1), ...`

```scala
val days = Array("Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday")
days.zipWithIndex.foreach {
    case(day, count) => println(s"$count is $day")
} //如果使用map，则返回的也是array数组，即利用zipWithIndex，将序号考虑进来进行操作
```

```
0 is Sunday
1 is Monday
2 is Tuesday
3 is Wednesday
4 is Thursday
5 is Friday
6 is Saturday
```

## groupby

对集合中的元素进行分组操作，结果是得到一个Map，`def groupBy[K](f: (A) ⇒ K): Map[K, List[A]]`

```
scala> List((1,2),(1,3),(2,3),(3,3),(3,4)).groupBy(_._1)
res1: scala.collection.immutable.Map[Int,List[(Int, Int)]] = Map(2 -> List((2,3)), 1 -> List((1,2), (1,3)), 3 -> List((3,3), (3,4)))
```

该方法的用途是：**通过一个给定的函数（用逗号接在后面）**，依次把集合中的每一个元素转换（或者说映射）成一个值（类型是K），后续同样映射出这个值的元素会和前面的元素一起放到一个List里，这样最终的返回结果是一个map，**map的key是通过传入的函数映射出的key**, map的value是所有映射出相同key的元素集合（一个List）。

很多时候我们可能会利用这个方法将集合中的元素进行分组，针对一个分组（也就是每一个唯一的元素），算出重复的元素的数量，代码如下：
```
scala> val a: Array[Int] = Array(1, 12, 3, 4, 1)
a: Array[Int] = Array(1, 12, 3, 4, 1)

scala> a.groupBy(i=>i)
res1: scala.collection.immutable.Map[Int,Array[Int]] = Map(4 -> Array(4), 1 -> Array(1, 1), 3 -> Array(3), 12 -> Array(12))

scala> a.groupBy(i=>i).mapValues { _.length }
res2: scala.collection.immutable.Map[Int,Int] = Map(4 -> 1, 1 -> 2, 3 -> 1, 12 -> 1)
```
上述代码中i=>i就是identity函数的一个适用的例子，由于在这里分组的逻辑是非常简单的，但是groupBy需要的又必须是一个函数，所以我们手写了i=>i这样看上去很怪异的函数字面量。如果我们使用预定义的identity函数，则一切变得自然和优雅了：
```
scala> a.groupBy(identity)
res3: scala.collection.immutable.Map[Int,Array[Int]] = Map(4 -> Array(4), 1 -> Array(1, 1), 3 -> Array(3), 12 -> Array(12))

scala> a.groupBy(identity).mapValues { _.length }
res4: scala.collection.immutable.Map[Int,Int] = Map(4 -> 1, 1 -> 2, 3 -> 1, 12 -> 1)
```

##mapValues

对map进行操作，只修改map的value

```scala
val m = Map( "a" -> 2, "b" -> 3 )
m.mapValues(_ * 5)
```

```
res0: scala.collection.immutable.Map[String,Int] = Map(a -> 10, b -> 15)
```

## Reference

- [scala school](https://twitter.github.io/scala_school/collections.html)
- [scala函数组合器](https://blog.csdn.net/springlustre/article/details/52882205)
- [identity](https://blog.csdn.net/bluishglc/article/details/52806646 )