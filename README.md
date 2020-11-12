## Enron Mail Analysis

Code Build:
Created in Python 3.4.3 and compatable with spark >2.20

Dependencies:
At Line 31 the path to the dir where the files are stored need to be specified
There is only one dependency that needs to be added pandas (optional code and be written without it as well)

Command:
spark-submit main.py 

Design Consideration:

We have used Pyspark in the above solution as it can scale horizontally in case the data explodes. it workes on the map reduce paradigm and hence would easily scale without exploding the cost.In the case were the data increase the executore needed to adjusted to allow the program to scale

In the pyspark Program we have tried to parameterize as much as possible . the extractions process fetches all the files in the folders recursively. so that all the emails have been read.we use the email package to parse the email metadata and use the explode function to get the to field in a single column value. Below are the further process we have done to imporve the runtime performance



1. The codes uses UDF to make all the operation scale
2. we Cache and persist the table after joing to avoid latency issues
3. To improve the code the files should be stored in parquet format for easy access
4. for scaling purpose we can tune the number of executors to scale up
5. We can run this on aws emr with autoscaling enabled to scale on Demand 
6. For easier access the tables can be created directly in Apache Hive


Assumptions:

1. The Time is at Seconds level hene Q3 has been calculated in seconds and the converted Ms
2. we assume the files are going to be in present in the folder structed unzipped for access
