

Data Serialization is the process of converting the in-memory object to another format that can be used to store in a file or send over the network. It plays a distinctive role in the performance of any distributed application. The computation gets slower due to formats that are slow to serialize or consume a large number of files. Apache Spark gives two serialization libraries:

- Java serialization
- Kryo serialization


Serialization plays an important role in the performance for any distributed application. By default, Spark uses Java serializer.
Spark can also use another serializer called ‘Kryo’ serializer for better performance.
Kryo serializer is in compact binary format and offers processing 10x faster than Java serializer.
To set the serializer properties:
conf.set(“spark.serializer”, “org.apache.spark.serializer.KryoSerializer”)


![image](https://user-images.githubusercontent.com/32897934/120025782-d32dc780-c00e-11eb-9a3e-4fc48663d565.png)
