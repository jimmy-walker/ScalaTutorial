# Date

```scala
import java.text.SimpleDateFormat
import java.util.Calendar
import scala.collection.mutable.ListBuffer
val date_end = args(0) //2017-12-09
val period = 29
val date_period = getDaysPeriod(date_end, period)
val date_start = date_period.takeRight(1)(0)
// get the period days under date_start and interval in List[String] format
def getDaysPeriod(dt: String, interval: Int): List[String] = {
	var period = new ListBuffer[String]() //initialize the return List period
	period += dt
	val cal: Calendar = Calendar.getInstance() //reset the date in Calendar
	cal.set(dt.split("-")(0).toInt, dt.split("-")(1).toInt - 1, dt.split("-")(2).toInt)
	val dateFormat: SimpleDateFormat = new SimpleDateFormat("yyyy-MM-dd") //format the output date
	for (i <- 0 to interval - 1){
	  cal.add(Calendar.DATE, - 1)
	  period += dateFormat.format(cal.getTime())
	}
	period.toList
}
```

