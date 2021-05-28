What is Coalesce?
The coalesce method reduces the number of partitions in a DataFrame. Coalesce avoids full shuffle, instead of creating new partitions, it shuffles the data using Hash Partitioner (Default), and adjusts into existing partitions, this means it can only decrease the number of partitions.

What is Repartitioning?
The repartition method can be used to either increase or decrease the number of partitions in a DataFrame. Repartition is a full Shuffle operation, whole data is taken out from existing partitions and equally distributed into newly formed partitions.

![image](https://user-images.githubusercontent.com/32897934/120019060-9c06e880-c005-11eb-9f3c-78c4725e5745.png)


Where to use what?
Let’s look at the below example for the answer.
![image](https://user-images.githubusercontent.com/32897934/119974516-6268ba00-bfd2-11eb-998b-17d886daa422.png)


Now, if I manually pass the number of partitions to 10, see how the data gets distributed:

![image](https://user-images.githubusercontent.com/32897934/119974534-67c60480-bfd2-11eb-84d7-8e9342db44ea.png)
![image](https://user-images.githubusercontent.com/32897934/119974546-6bf22200-bfd2-11eb-82da-5757019791a9.png)


Comparatively, coalesce took less time as compared with repartitioning. And the data gets partitioned as below:
Screenshot 2021-05-28 at 4.33.35 PM![image](https://user-images.githubusercontent.com/32897934/119974607-7d3b2e80-bfd2-11eb-83e3-3acb77566e48.png)


If you observe above table when repartitioned, data over all the partitions are equally populated, but when we used coalesce the data is not equally distributed.

Also, if you observed above coalesce didn’t partition your data to 10 partitions instead it created 6 partitions. That means even if you provide a large number of partitions, it partitions your data to the default one in the above case it is 6.

Now we understand the behavior and hence back to our initial question, where to use which function?

Coalesce use case: we pass in all 10 above partitions into our RDD and perform some action, the partition which processes the file part-00000 will finish first followed by others but the executor with part-00005 will be still running meanwhile 1st executor will be idle. Hence, the load is not balanced on executors equally.

Repartition use case: All the executors finish the job at the same time, and the resources are consumed equally because all input partitions have the same size.

So, here is the answer:
If you have loaded a dataset, includes huge data, and a lot of transformations that need an equal distribution of load on executors, you need to use Repartition.
Once all the transformations are applied and you want to save all the data into fewer files(no. of files = no.of partitions) instead of many files, use coalesce.
So, this was all about Repartitioning & Coalesce. Hope to take the inputs from this blog you gonna better partition your data now to increase your Job performance.

