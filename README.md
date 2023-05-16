# spark-playground

## Null, None
None is an object in python, NoneType, if you perform == or != operation with two None values, it always results in False. That is the key reason `isNull()` or `isNotNull()` functions are built for. <br>
eg.

    lst = [(1,'sometext'),(2,''),(3, None),(4, 'someothertext')]

    rdd = sc.parallelize(lst).map(lambda x: Row(id=x[0], txt=x[1]))
    df= sqlContext.createDataFrame(myrdd)
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
