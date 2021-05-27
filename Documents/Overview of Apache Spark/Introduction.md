Apache Spark - The largest open source project in data processing.
Spark is framework and is mainly used on top of other systems. You can run Spark using its standalone cluster mode 
on EC2, 
on Hadoop YARN, 
on Mesos, or 
on Kubernetes.


![image](https://user-images.githubusercontent.com/32897934/119866711-b922b500-bf3a-11eb-8577-52b6c9ea9580.png)

Components of Spark
components of Spark ecosystem like Spark core component, Spark SQL, Spark Streaming, Spark MLlib, Spark GraphX and SparkR.
Apache Spark Core:
The key features of Apache Spark Core are:

- It is in charge of essential I/O functionalities.
- Significant in programming and observing the role of the Spark cluster.
- Task dispatching.
- Fault recovery.
- It overcomes the snag of MapReduce by using in-memory computation.

Spark Core is embedded with a special collection called RDD (resilient distributed dataset).
RDD - partitioning of data across all nodes
operations performed on RDDs: 
- Transformation: It is a function that produces new RDD from the existing RDDs.
2 groups of transformations can be applied to RDD, namely narrow transformations, and wide transformations.
  - narrow transformations: Narrow transformation does not require shuffle or reorganizing data between partitions. For example, map',filter', etc. Narrow transformations will be stacked together, allowing such transformations to be performed in parallel on different partitions.
  - Wide transformations: such as groupByKey, reduceByKey, etc. Within these transformations, the data needed for the processing can be located in several partitions of the parent RDD that need to be combined. To implement these operations, Spark must perform a shuffle by moving data across the cluster and forming a new stage with a new set of partitions


- Action: In Transformation, RDDs are created from each other. But when we want to work with the actual dataset, then, at that point we use Action.

DAG - Spark defines tasks that can be computed in parallel with the partitioned data on the cluster. With these defined tasks, Spark builds a logical flow of operations that can be represented as a directional and acyclic graph, also known as DAG (Directed Acyclic Graph), where the node represents an RDD partition and the edge represents a data transformation.


![image](https://user-images.githubusercontent.com/32897934/119869102-7b735b80-bf3d-11eb-954b-9d96fbe7cf29.png)

The following figure gives a detailed explanation of the differences between processing in Spark and Hadoop.
![image](https://user-images.githubusercontent.com/32897934/119867659-be343400-bf3b-11eb-9eaa-e6ab405dafad.png)
![image](https://user-images.githubusercontent.com/32897934/119867665-c3917e80-bf3b-11eb-86fd-b2735641eefd.png)

![image](https://user-images.githubusercontent.com/32897934/119867967-15d29f80-bf3c-11eb-9095-c1392af1e9c5.png)



