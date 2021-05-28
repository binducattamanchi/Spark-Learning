Spark Memory Management:

![image](https://user-images.githubusercontent.com/32897934/119886460-9f8c6800-bf50-11eb-8cb9-28aff186004d.png)

Executor Container:

When submitting a Spark job in a cluster with Yarn, Yarn allocates Executor containers to perform the job on different nodes.

ResourceManager handles memory requests and allocates executor container up to maximum allocation size settled by yarn.scheduler.maximum-allocation-mb configuration. Memory requests higher than the specified value will not take effect.

On a single node, it is done by NodeManager. NodeManager has an upper limit of resources available to it because it is limited by the resources of one node of the cluster. In Yarn it set up by yarn.nodemanager.resource.memory-mb configuration. It is the amount of physical memory per NodeManager, in MB, which can be allocated for yarn containers

![image](https://user-images.githubusercontent.com/32897934/119886539-b632bf00-bf50-11eb-9d56-00f55261c527.png)




- OnHeap Memory vs OffHeap Memory:

![image](https://user-images.githubusercontent.com/32897934/119886312-753aaa80-bf50-11eb-8601-468dae447a18.png)


![image](https://user-images.githubusercontent.com/32897934/119886313-753aaa80-bf50-11eb-85d6-d7d1272ff3b7.png)



More details: https://luminousmen.com/post/dive-into-spark-memory/
