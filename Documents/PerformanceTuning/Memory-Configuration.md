http://spark-configuration.luminousmen.com/
https://spoddutur.github.io/spark-notes/distribution_of_executors_cores_and_memory_for_spark_application.html
http://site.clairvoyantsoft.com/understanding-resource-allocation-configurations-spark-application/

- Running executors with too much memory often results in excessive garbage collection delays.
- Running tiny executors (with a single core and just enough memory needed to run a single task, for example) throws away the benefits that come from running multiple tasks in a single JVM.

- Couple of recommendations to keep in mind which configuring these params for a spark-application like:
> Budget in the resources that Yarn’s Application Manager would need.
> How we should spare some cores for Hadoop/Yarn/OS deamon processes
> Learnt about spark-yarn-memory-usage

- Also, checked out and analysed three different approaches to configure these params:
> Tiny Executors - One Executor per Core. 
> Fat Executors - One executor per Node. 
> Recommended approach - Right balance between Tiny (Vs) Fat coupled with the recommendations.

--num-executors, --executor-cores and --executor-memory.. these three params play a very important role in spark performance as they control the amount of CPU & memory your spark application gets. This makes it very crucial for users to understand the right way to configure them.
