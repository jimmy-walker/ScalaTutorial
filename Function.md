# Scala Function

## toMap

```scala
def toMap[T, U]: Map[T, U]
//convert this array to map
```

注意需要保证array中每个都是tuple，有两个数据。


```scala
scala> val xs = Array(20140101,20140102,20140103,20140104,20140105,20140106,20140107,20140108)          
xs: Array[Int] = Array(20140101, 20140102, 20140103, 20140104, 20140105, 20140106, 20140107, 20140108)

scala> xs.map(x => "s3://" + x).grouped(3).zipWithIndex.map(t => (t._2, t._1)).toMap
res16: scala.collection.immutable.Map[Int,Array[String]] = Map(0 -> Array(s3://20140101, s3://20140102, s3://20140103), 1 -> Array(s3://20140104, s3://20140105, s3://20140106), 2 -> Array(s3://20140107, s3://20140108))
```

