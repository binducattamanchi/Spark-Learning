
![image](https://user-images.githubusercontent.com/32897934/119882919-98fbf180-bf4c-11eb-9145-adb2f4bf1d26.png)


Screenshot 2021-05-28 at 12.38.47 AM![image](https://user-images.githubusercontent.com/32897934/119884393-37d51d80-bf4e-11eb-85bf-0a331f647a3d.png)


**Broadcast Variables**
Broadcast variables are read-only variables that will be cached in all the executors instead of shipping every time with the tasks. Basically, broadcast variables are used as lookups without any shuffle, as each executor will keep a local copy of it, so no network I/O overhead is involved here. Imagine you are executing a Spark Streaming application and for each input event, you have to use a lookup data set which is distributed across multiple partitions in multiple executors; so, each event will end up doing network I/O that will be a huge, costly operation for a streaming application with such frequency.  

Now, the question is how big of a lookup dataset do you want to broadcast!! The answer lies in the amount of memory you are allocating for each executor. See, if we broadly look at memory management in Spark, we'll observe that Spark keeps 75% of the total memory for its own storage and execution. Out of that 75%, 50% is allocated for storage purposes, and the other 50% is allocated for execution purposes. 

![image](https://user-images.githubusercontent.com/32897934/119885105-027cff80-bf4f-11eb-8394-fdbcac40a086.png)

For example, if you allocate 10 GB memory to an executor, then according to the formula, you Spark storage memory would be :

 (“Java Heap” – 300MB) * 0.75 * 0.5 = 3.64GB(approx) 
[ 300MB is reserved memory ]  

Spark stores broadcast variables in this memory region, along with cached data. There is a catch here. This is the initial Spark memory orientation. If Spark execution memory grows big with time, it will start evicting objects from a storage region, and as broadcast variables get stored with MEMORY_AND_DISK persistence level, there is a possibility that it also gets evicted from memory. So, you could potentially end up doing disk I/O, which is again a costly operation in terms of performance. 

So, the bottom line is, we have to carefully choose the size of the broadcast variables keeping all this in mind. If you want to know more about Spark memory management, please check this blog Spark memory management.

So, in the end, we can say that through accumulators, Spark gives executors provision to coordinate values with each other; whereas through broadcast variables, it provides the same dataset across multiple stages without shuffling.

**Accumulators**
Accumulators are a special kind of variable that we basically use to update some data points across executors. One thing we really need to remember is that the operation by which the data point update happens has to be an associated and commutative operation. Let's take an example to have a better understanding of accumulator:

Lets say, you have a big text file, and you need to find out the count of the number of lines containing  "_".

This is a good scenario where you can use an accumulator. So, first, we'll read the file which will create an RDD out of it.

Scala : val inputRdd = sc.textFile("D:\\intelliJ-Workspace\\spark_application\\src\\main\\sampleFileStorage\\rawtext")

It will distribute the file in multiple partitions across all the executors. Now, we need to create an accumulator in the driver. We will be using an Accumulator of type Long, as we are going to count the lines with '_'.

Scala : val acc = sc.longAccumulator("Underscore Counter")

Now, we will check if each line of the inputRdd contains '_' and increase the accumulator count by 1 if we find it. so, in the end, if we print the value of the accumulator, will see the exact count of lines having '_'.

Scala: inputRdd.foreach { line =>
  if (line.contains("_"))
    acc.add(1)
}
println(acc.value);

So, the bottom line is when you want Spark workers to update some value, you should go with accumulator. For more details regarding accumulator.

