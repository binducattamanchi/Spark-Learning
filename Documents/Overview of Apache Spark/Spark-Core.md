
Apache Spark Core:
The key features of Apache Spark Core are:

- It is in charge of essential I/O functionalities.
- Significant in programming and observing the role of the Spark cluster.
- Task dispatching.
- Fault recovery.
- It overcomes the snag of MapReduce by using in-memory computation.

Spark Core is embedded with a special collection called RDD (resilient distributed dataset).
RDD - logical partitioning of data across all nodes
RDDs are the building blocks of any Spark application. RDDs Stands for:

 - Resilient: Fault tolerant and is capable of rebuilding data on failure
 - Distributed: Distributed data among the multiple nodes in a cluster
 - Dataset: Collection of partitioned data with values


It is a layer of abstracted data over the distributed collection. It is immutable in nature and follows lazy transformations. 

![image](https://user-images.githubusercontent.com/32897934/119876872-fb9dbf00-bf45-11eb-94ea-cf7b6d9d0dad.png)


operations performed on RDDs: 
- Transformation: It is a function that produces new RDD from the existing RDDs.
2 groups of transformations can be applied to RDD, namely narrow transformations, and wide transformations.
  - narrow transformations: Narrow transformation does not require shuffle or reorganizing data between partitions. For example, map',filter', etc. Narrow transformations will be stacked together, allowing such transformations to be performed in parallel on different partitions.
  - Wide transformations: such as groupByKey, reduceByKey, etc. Within these transformations, the data needed for the processing can be located in several partitions of the parent RDD that need to be combined. To implement these operations, Spark must perform a shuffle by moving data across the cluster and forming a new stage with a new set of partitions

![image](https://user-images.githubusercontent.com/32897934/119871650-4ae0f100-bf40-11eb-8328-90d9ed7eac4d.png)


- Action: In Transformation, RDDs are created from each other. But when we want to work with the actual dataset, then, at that point we use Action.


![image](https://user-images.githubusercontent.com/32897934/119876755-da3cd300-bf45-11eb-8fa0-8d39529b01c6.png)


DAG - Spark defines tasks that can be computed in parallel with the partitioned data on the cluster. With these defined tasks, Spark builds a logical flow of operations that can be represented as a directional and acyclic graph, also known as DAG (Directed Acyclic Graph), where the node represents an RDD partition and the edge represents a data transformation.

Screenshot 2021-05-27 at 11.08.27 PM![image](https://user-images.githubusercontent.com/32897934/119871850-7e238000-bf40-11eb-8d03-583cfd332305.png)


