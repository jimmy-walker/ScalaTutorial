# Syntactic sugar

对于scala搞那么多语法糖和新概念真是又爱又恨。爱的是scala引入了java一直没有的lambda特性，这对于使用高阶函数抽象来处理集合数据非常有爱（spark简洁的RDD处理得益于此）。恨的是scala搞那么多的新概念和语法糖。  

##点号省略

```scala
//无参数  
"hello" toUpperCase  
"hello".toUpperCase  
"hello".toUpperCase()  
//一个参数  
"hello".indexOf "h"  
"hello" indexOf "h"   
//多个参数  
"hello world" substring (0, 3)   
//全部搞在一起  
 "hello world" substring (0, 3)  toUpperCase() indexOf "h"  
//配合上匿名函数  
Array(1,2,3) map ((i:Int)=> i+1)  
 1 to 3 map ((i:Int)=> i+1)  
```

## for

```scala
//这个for挺正常的吧？  
for(i <- 1 to 4) println(i)  
//这个呢！  
 for(i <- 1 to 4 if i > 1) println(i)  
//这个呢！！！  
 for(i <- 1 to 4 if i > 1; if i < 4; if i % 2 ==0) println(i)  
```

##花括号代替小括号
```scala
println("hello")  
println{"hello"}  
  
def xx(i:Int)(j:Int) = i+j  
 xx(1){2} //result: 3  
(xx(1)_){3} //curry化调用  
(xx(1)_)(3) //curry化调用，不信你不懵  
  
//看了上面的还没懵？那就再来个  
def xx(i:Int)(j:(Int)=>Int) = j(i)  
xx(1){i=> i+10}  
  
//有爱的一面  
//假设我定义一个hbase的scan方法  
def scan(tableName:String, cf:String, startRow:String, stopRow:String)(processFn:(Result)=>Unit) = {  
  //...  
}  
//那么我可以这么自然的调用  
scan(t1, cf, startRow, stopRow){ r =>  
   //TODO process result  
}  
```

## Reference

- [关于scala搞出的新概念和语法糖](https://clojure.iteye.com/blog/2091818)