# List

## List求和：reduceLeft
比如`val tmp = （a1, a2, a3, ... an)`
tmp.reduceLeft 会按照如下的步骤执行：
先计算f(a1,a2) ,其中f是一个函数，这个函数是作为tmp.reduceLeft的参数传进去的；
然后tmpa <- f(a1,a2) ；
接着tmpa <- f(tmpa, a3) ；
直到tmpa <- f(tmpa, an)；
最后tmp.reduceLeft返回tmpa。

```scala
def weighted_average(index: List[Int], weights: List[Double], w: WindowSpec, c: Column): Column= {
  val wma_list = for (i <- index) yield (lag(c, i).over(w))*weights(i) // list comprehension, map also can do same things, return scala.collection.immutable.IndexedSeq
  wma_list.reduceLeft(_ + _)
}
```

## List是不可变，可用List buffer

How do I add elements to a Scala `List`?

This is actually a trick question, because you *can't* add elements to a Scala [List](http://www.scala-lang.org/api/current/scala/collection/immutable/List.html); it's an immutable data structure, like a Java `String`.

If you want to use a Scala sequence that has many characteristics of a `List`and is also *mutable* — i.e., you can add and remove elements in it — the correct approach is to use the [ListBuffer](http://www.scala-lang.org/api/current/scala/collection/mutable/ListBuffer.html) class instead, like this:

```
import scala.collection.mutable.ListBuffer
var fruits = new ListBuffer[String]()
fruits += "Apple"
fruits += "Banana"
fruits += "Orange"
```

Then convert it to a `List` if/when you need to:

```
val fruitsList = fruits.toList
```
