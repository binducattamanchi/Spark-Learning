
![image](https://user-images.githubusercontent.com/32897934/119875713-b200a480-bf44-11eb-95ef-94da6fe029f9.png)

![image](https://user-images.githubusercontent.com/32897934/119875745-bcbb3980-bf44-11eb-91fb-bfd457892dbc.png)


The components of the spark application are:

- Driver
- Application Master
- Spark Context
- Cluster Resource Manager(aka Cluster Manager)
- Executors

Spark uses a master/slave architecture with a central coordinator called Driver and a set of executable workflows called Executors that are located at various nodes in the cluster.

**Driver**
The Driver(aka driver program) is responsible for converting a user application to smaller execution units called tasks and then schedules them to run with a cluster manager on executors. The driver is also responsible for executing the Spark application and returning the status/results to the user.

Spark Driver contains various components – DAGScheduler, TaskScheduler, BackendScheduler and BlockManager. They are responsible for the translation of user code into actual Spark jobs executed on the cluster.

Other properties of Driver:
- can run in an independent process or on one of the work nodes for High Availability (HA);
- stores metadata about all Resilient Distributed Databases and their partitions;
- is created after the user sends the Spark application to the cluster manager (YARN in our case);
- runs in its own JVM;
- optimizes logical DAG transformations and, if possible, combines them in stages and determines the best location for execution of this DAG;
- creates Spark WebUI with detailed information about the application;

**Application Master**





