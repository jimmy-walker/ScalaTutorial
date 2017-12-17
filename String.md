# String

## <u>**字符串插值's'和$，一定要是双引号。**</u>

文字`'s'`允许在处理字符串时直接使用变量。任何在范围中的String变量可以在字符串中使用。以下是`'s'`字符串插值器的用法。

```scala
val name = "James"
println(s"Hello, $name") //output: Hello, James
```




## <u>String是不可变的，用StringBuilder</u>

**StringBuilder.** In a string append, a new string must be created. A string cannot be changed. But with StringBuilder we add data to an internal buffer. This makes things faster.

```scala
val builder = StringBuilder.newBuilder // Create a new StringBuilder.
for (dt <- date_period){
	builder.append(s"(1, $dt)")
}
val result = builder.toString() // Convert StringBuilder to a string.
println(result)
```

