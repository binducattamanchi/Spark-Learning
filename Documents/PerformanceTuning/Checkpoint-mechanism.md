**checkpoint concept**
We can cache the data of rdd and store it in memory or disk. They can be obtained directly from memory or disk, but they are not particularly secure.

**cache**

It directly saves the data in the memory, and the subsequent operation is faster, and gets it directly from the memory. However, this method is not safe, because the server is hung up or the process is terminated, it will lead to the loss of data.

**persist**

It can save the data in the local disk, and then get the data from the disk. However, it is not particularly secure. Due to some errors of the system administrator, the deletion, or the disk damage, may also lead to the loss of data.

**checkpoint**

It provides a relatively more reliable way of data persistence. It stores data on a distributed file system, such as HDFS. Here is the use of HDFS high availability, high fault tolerance (multiple copies) to maximize data security.

**Differences among cache, persist and checkpoint**
**cache and persist**

Cache the default data cache is in memory
persist can save data in memory or disk
To trigger cache and persist persistence operations, an action operation is required
It does not open other new tasks, and an action operation corresponds to a job
It does not change the dependency of rdd, and the corresponding cache data will disappear automatically after the program runs
**checkpoint**

Data can be persisted and written to hdfs

In order to trigger the checkpoint persistence operation in the future, an action operation is required, and a new job will be opened to perform checkpoint operation

It will change the dependency of rdd, and subsequent data loss cannot be recovered through lineage.

After the program runs, the corresponding checkpoint data will not disappear
