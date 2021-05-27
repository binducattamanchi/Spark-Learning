Spark introduced three types of API to work upon – RDD, DataFrame, DataSet
RDD is used for low level operation with less optimization
DataFrame is best choice in most cases due to its catalyst optimizer and low garbage collection (GC) overhead.
Dataset is highly type safe and use encoders.  It uses Tungsten for serialization in binary format.
We know that Spark comes with 3 types of API to work upon -RDD, DataFrame and DataSet.

RDD is used for low-level operations and has less optimization techniques.

DataFrame is the best choice in most cases because DataFrame uses the catalyst optimizer which creates a query plan resulting in better performance. DataFrame also generates low labor garbage collection overhead.

DataSets are highly type safe and use the encoder as part of their serialization. It also uses Tungsten for the serializer in binary format.
