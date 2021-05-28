![image](https://user-images.githubusercontent.com/32897934/119878446-bed2c780-bf47-11eb-9c3e-1e75269311dd.png)
![image](https://user-images.githubusercontent.com/32897934/119878586-f04b9300-bf47-11eb-9951-e0632f92fb99.png)

STEP 1: The client submits spark user application code. When an application code is submitted, the driver implicitly converts user code that contains transformations and actions into a logically directed acyclic graph called DAG. At this stage, it also performs optimizations such as pipelining transformations.

STEP 2: After that, it converts the logical graph called DAG into physical execution plan with many stages. After converting into a physical execution plan, it creates physical execution units called tasks under each stage. Then the tasks are bundled and sent to the cluster.

STEP 3: Now the driver talks to the cluster manager and negotiates the resources. Cluster manager launches executors in worker nodes on behalf of the driver. At this point, the driver will send the tasks to the executors based on data placement. When executors start, they register themselves with drivers. So, the driver will have a complete view of executors that are executing the task.

STEP 4: During the course of execution of tasks, driver program will monitor the set of executors that runs. Driver node also schedules future tasks based on data placement. 


Spark-Submit process explained with example:
https://www.edureka.co/blog/spark-architecture/


1. When we send the Spark application in cluster mode, the spark-submit utility communicates with the Cluster Resource Manager to start the Application Master.
2. The Resource Manager is then held responsible for selecting the necessary container in which to run the Application Master. The Resource Manager then tells a specific Node Manager to launch the Application Master.
3. The Application Master registers with the Resource Manager. Registration allows the client program to request information from the Resource Manager, that information allows the client program to communicate directly with its own Application Master.
4. The Spark Driver then runs on the Application Master container (in case of cluster mode).
5. The driver implicitly converts user code containing transformations and actions into a logical plan called a DAG. All RDDs are created in the driver and do nothing until the action is called. At this stage, the driver also performs optimizations such as pipelining narrow transformations.
6. It then converts the DAG into a physical execution plan. After conversion to a physical execution plan, the driver creates physical execution units called tasks at each stage.
7. The Application Master now communicates with the Cluster Manager and negotiates resources. Cluster Manager allocates containers and asks the appropriate NodeManagers to run the executors on all selected containers. When executors run, they register with the Driver. This way, the Driver has a complete view of the artists.
8. At this point, the Driver will send tasks to executors via Cluster Manager based on the data placement.
9. The code of the user application is launched inside the container. It provides information (stage of execution, status) to the Application Master.
10. At this stage, we will start to execute our code. Our first RDD will be created by reading data in parallel from HDFS to different partitions on different nodes based on HDFS InputFormat. Thus, each node will have a subset of data.
11. After reading the data we have two map transformations which will be executed in parallel on each partition.
12. Next, we have a reduceByKey transformation, it is not a narrow transformation like map, so it will create an additional stage. It combines records with the same keys, then moves data between nodes (shuffle) and partitions to combine the keys of the same record.
13. We then perform an action — write back to HDFS which will trigger the entire DAG execution.
14. During the execution of the user application, the client communicates with the Application Master to obtain the application status.
15. When the application finishes executing and all of the necessary work is done, the Application Master disconnects itself from the Resource Manager and stops, freeing up its container for other purposes.


