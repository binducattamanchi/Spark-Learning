
Serialization plays an important role in the performance for any distributed application. By default, Spark uses Java serializer.
Spark can also use another serializer called ‘Kryo’ serializer for better performance.
Kryo serializer is in compact binary format and offers processing 10x faster than Java serializer.
To set the serializer properties:
conf.set(“spark.serializer”, “org.apache.spark.serializer.KryoSerializer”)

 

Code:
val conf = new SparkConf().setMaster(…).setAppName(…)

conf.registerKryoClasses(Array(classOf[MyClass1], classOf[MyClass2]))

val sc = new SparkContext(conf)

 

Serialization plays an important role in the performance of any distributed application and we know that by default Spark uses the Java serializer on the JVM platform. Instead of Java serializer, Spark can also use another serializer called Kryo. The Kryo serializer gives better performance as compared to the Java serializer.

Kryo serializer is in a compact binary format and offers approximately 10 times faster speed as compared to the Java Serializer. To set the Kryo serializer as part of a Spark job, we need to set a configuration property, which is org.apache.spark.serializer.KryoSerializer.
