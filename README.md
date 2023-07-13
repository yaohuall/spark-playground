# spark-playground

## Null, None
None is an object in python, NoneType, if you perform == or != operation with two None values, it always results in False. That is the key reason `isNull()` or `isNotNull()` functions are built for. <br>
eg.

    lst = [(1,'sometext'),(2,''),(3, None),(4, 'someothertext')]

    rdd = sc.parallelize(lst).map(lambda x: Row(id=x[0], txt=x[1]))
    df= sqlContext.createDataFrame(rdd)
isNull() returns True for Row#3, thus below statement returns one row 

    mydf.filter(col("txt").isNull()).show(truncate=False)
    +---+----+
    |id |txt |
    +---+----+
    |3  |null|
    +---+----+
== operator returns False for Row#3, thus no records are filtered out.

    mydf.filter(col("txt") == None).show(truncate=False)
    +---+---+
    |id |txt|
    +---+---+
    +---+---+

## Run Spark on K8s
### SPARK configs
- SPARK_WORKER_CORES: CPU cores you can use per worker process, in Helm Chart, use with Values.corelimit parameter.
- SPARK_WORKER_INSTANCES: number of worker process in each worker node
#### Only if you have large cluster, then use multiple worker process

### reference
https://stackoverflow.com/questions/24696777/what-is-the-relationship-between-workers-worker-instances-and-executors
https://spark.apache.org/docs/latest/running-on-kubernetes.html <br>
https://medium.com/rahasak/spark-cluster-deployment-with-kubernetes-1848d061cfc9
