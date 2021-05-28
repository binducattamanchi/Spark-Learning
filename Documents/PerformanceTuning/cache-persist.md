
![image](https://user-images.githubusercontent.com/32897934/120021080-39fbb280-c008-11eb-900d-7fb580c3bb1a.png)

The cache execution can only be triggered after an action.

The differences between the cache method and the persist method are as follows:

cache: by default, the data is cached in memory, and its essence is to call the persist method;
persist: data can be cached in memory or disk. There are rich cache levels. These cache levels are defined in the object of StorageLevel.
