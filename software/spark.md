# spark basic

$ spark-shell

val a = sc.parallelize(1 to 9, 3)
val data = Array(1, 2, 3, 4, 5)
data.foreach(x => print(x+" "))

val distData = sc.parallelize(data)

distData.foreach(x => print(x+" "))
distData.take(100).foreach(println)
distData.collect().foreach(println)

val mapData = distData.map(v => v+1)
> for (item <- mapData) print(item + " ")

scala> val flatMapData = distData.flatMap(x => 1 to x)
flatMapData.foreach(print)

var partitionData = distData.mapPartitions(x => x.filter(_>=3))

val glomData = distData.glom()
glomData.foreach(x => x.foreach(println))

val distData2 = sc.parallelize(Array(2,3,4,5,6,11))
val unionData = distData.union(distData2)

val cartesianData = distData.cartesian(distData2)

val fData = distData.filter(x => x>3)

val dData = sc.parallelize(Array(1,1,2,2)).distinct()

val distDict = sc.parallelize(List(("A",1),("B",2),("c",3),("A",4),("C",5) ))
val mapDict = distDict.mapValues(x => x+2)

val reduceDict = distDict.reduceByKey((a,b) => a+b)


# word count

val textFile = sc.textFile("/home/frank/swift-git-log.txt")
val counts = textFile.flatMap(line => line.split(" "))
>					.map(word => (word, 1))
>					.reduceByKey(_ + _)
counts.saveAsTextFile("/home/frank/spark-word-counts") // 目录

# topK

val  topk= counts.mapPartitions(iter=>{
while(iter.hashNext){
    putToHeap(iter.next())
}
getHeap().iterator
}).collect()


val heap = scala.collection.mutable.ListBuffer.empty[(String, Int)]
> def cmp(a:(String, Int), b:(String, Int)) = (a._2 < b._2)

val topK = counts.mapPartitions(iter => {
while(iter.hasNext){
	heap += iter.next()
}
val newHeap = heap.sortWith(cmp)
newHeap.iterator
}).collect()
	








