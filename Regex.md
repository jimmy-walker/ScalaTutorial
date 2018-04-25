# regex expression

## 使用scala的正则表达式

- 匹配多规则时，只能使用分枝条件（branch condition），[没有别的办法。](https://stackoverflow.com/questions/3050907/scala-capture-group-using-regex)
- 在规定字符附近的匹配，要么使用分组（group），要么断言。
- 可以调用`reg.findAllIn(str).length > 0`来判断是否匹配到。
- 分组：group(0) returns the full match, group(1) returns the first capture (within parentheses), group(2) returns the second capture and so on.
- 注意：**<u>Iterators in scala are single-used - once you traversed it (e.g. by applying `length` method) it becomes empty. You can fix that behavior by converting to List, or to Seq (lazy):</u>**
- **<u>这里理解为findAllIn后的长度，就是找到了几个，而matchData就是把这几个中给展开，看每个里面是否有group的结果。</u>**

```scala
val regex = "^G.E.M.邓紫棋$|^G.E.M.邓紫棋(?=、)|(?<=、)G.E.M.邓紫棋(?=、)|(?<=、)G.E.M.邓紫棋$".r
val test = "王菲、G.E.M.邓紫棋、林俊杰"
val a = regex.findAllIn(test)
a.foreach(println)
//val s = a.toList
//s.foreach(println)
//如果有group的话，可以调用a.groupCount会告诉你在原来的regex中有几个组，如果没有括号，就为0
a.matchData foreach { m => println(m.group(1)) }
```

## 使用java的正则表达式，可以得到位置

- 通过[该方法](https://stackoverflow.com/questions/8938498/get-the-index-of-a-pattern-in-a-string-using-regex)可以得到位置信息。

```scala
import java.util.regex.Matcher
import java.util.regex.Pattern
val regex = "^G.E.M.邓紫棋$|^G.E.M.邓紫棋(?=、)|(?<=、)G.E.M.邓紫棋(?=、)|(?<=、)G.E.M.邓紫棋$"
val test = "王菲、G.E.M.邓紫棋、林俊杰"
val pattern = Pattern.compile(regex)
val matcher = pattern.matcher(test)
var result = ""
if (matcher.find()){
  result = test3.substring(0, matcher.start()) + "邓紫棋" + test3.substring(matcher.end(), test3.length)
}
```

