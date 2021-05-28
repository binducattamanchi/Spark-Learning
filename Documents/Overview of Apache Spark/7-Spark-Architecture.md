
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

**Application Master/Spark Master**

Application Master is a framework-specific entity charged with negotiating resources with ResourceManager(s) and working with NodeManager(s) to perform and monitor application tasks. Each application running on the cluster has its own, dedicated Application Master instance.

Spark Master is created simultaneously with Driver on the same node (in case of cluster mode) when a user submits the Spark application using spark-submit.

The Driver informs the Application Master of the executor's needs for the application, and the Application Master negotiates the resources with the Resource Manager to host these executors.

In offline mode, the Spark Master acts as Cluster Manager.

**Spark Context**
Spark Context is the main entry point into Spark functionality, and therefore the heart of any Spark application. It allows Spark Driver to access the cluster through its Cluster Resource Manager and can be used to create RDDs, accumulators and broadcast variables on the cluster. Spark Context also tracks executors in real-time by sending regular heartbeat messages.

Spark Context is created by Spark Driver for each Spark application when it is first submitted by the user. It exists throughout the lifetime of the Spark application.

Spark Context stops working after the Spark application is finished. For each JVM only one Spark Context can be active. You must stop()activate Spark Context before creating a new one.

**Cluster Resource Manager**
Cluster Manager in a distributed Spark application is a process that controls, governs, and reserves computing resources in the form of containers on the cluster. These containers are reserved by request of Application Master and are allocated to Application Master when they are released or available.

Once the containers are allocated by Cluster Manager, the Application Master transfers the container resources back to the Spark Driver, and the Spark Driver is responsible for performing the various steps and tasks of the Spark application.

SparkContext can connect to different types of Cluster Managers. Now the most popular types are YARN, Mesos, Kubernetes or even Nomad. There is also Spark's own standalone cluster manager.

Executors
Executors are the processes at the worker's nodes, whose job is to complete the assigned tasks. These tasks are executed on the worker nodes and then return the result to the Spark Driver.

Executors are started once at the beginning of Spark Application and then work during all life of the application, this phenomenon is known as "Static Allocation of Executors". However, users can also choose to dynamically allocate executors where they can add or remove executors to Spark dynamically to match the overall workload (but this can affect other applications running on the cluster). Even if one Spark executor crashes, the Spark application can continue to work.

Performers provide storage either in-memory for RDD partitions that are cached (locally) in Spark applications (via BlockManager) or on disk while using localCheckpoint.

Other executor properties:

- stores data in a cache in a JVM heap or on disk
- reads data from external sources
- writes data to external sources
- performs all data processing



