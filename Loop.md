# Loop

## for循环

<u>**左箭头 <- 用于为变量 x 赋值,多个变量则用分号；隔开**。</u>

<u>Range 可以是一个数字区间表示 i to j ，或者 i until j，或者是集合，比如列表List</u>。**左箭头 <- 用于为变量 x 赋值**。
多个变量则用分号；隔开

```scala
for( x <- Range ){
   println(x);
}
for (i <- 0 to print_predict.length - 1) {
  println(print_predict(i)._1 + "\t" + print_predict(i)._2)
}
```

**<u>循环遍历List中元素，读取List中元素</u>**，这是不使用length的方法

```scala
for (dt <- date_period){
	println(dt)
}
a.takeRight(2)(0) //这样去取倒数第二个数字，我感觉这点没有python好用，但是网上说后面就会体现出scala的好处了。
```

##list comprehension
使用`List.range(0, length)`而非上述提到的Range的三种表达式，以保证格式。
或者使用map函数（对已有List进行操作）或for加yeild。

```scala
import scala.math.pow
var sum = 0.0
for (i <- 0 to length-1 ){
  sum += pow(0.5, i)
}
val weights = for (i <- 0 to length-1 ) yield pow(0.5, i)/sum // it will return scala.collection.immutable.IndexedSeq[Double]
val weights2 = for (i <- List.range(0, length) ) yield pow(0.5, i)/sum //it will return List[Double]
val numbers = List(1, 2, 3, 4)
val numbers2 = numbers.map{i => pow(0.5, i)}
val weights3 = List.range(0, length).map{i => pow(0.5, i)}
```

## foreach

**foreach什么都不做...只是用来遍历打印而已**
foreach很像map，但没有返回值。foreach仅用于有副作用[side-effects]的函数。

```scala
// J foreach什么都不做...只是用来遍历打印而已....！！！！！！！！！！！！！！！！！！！！！！！
val numbers = List(1, 2, 3, 4)
numbers.foreach((i: Int) => i * 2)
// 你可以尝试存储返回值，但它会是Unit类型（即void）
scala> val doubled = numbers.foreach((i: Int) => i * 2)
doubled: Unit = ()
```