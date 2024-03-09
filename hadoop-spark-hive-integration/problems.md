# Some... Problems 😡

## ERROR: “FAILED: Execution Error, return code 1 from org.apache.hadoop.hive.ql.exec.StatsTask” while insert data from hive

DescriptionOn a Hortonworks HDP 3.x cluster, when you run a Hive mapping in the native environment to write data to a Hive partitioned target containing an expression transformation with TO\_Date() function, the mapping fails with the following error :

```
FAILED: Execution Error, return code 1 from org.apache.hadoop.hive.ql.exec.StatsTask
```

To resolve this issue, set the custom property **hive.stats.column.autogather** set to **false** in **hive-site.xml**.
