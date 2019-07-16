---
title: Azure HDInsight Solutions | Apache Spark | Resource Allocation
description: How resource alloation works in HDInsight Spark Solutions
services: hdinsight
author: confusionblinds
ms.author: deeptivu
ms.service: hdinsight
ms.custom: troubleshooting
ms.topic: conceptual
ms.date: 7/15/2019
---
# Azure HDInsight Solutions | Spark | resource allocation

## Scenario: Spark activity running in Azure Data Factory fails with IllegalArgumentException

## Issue

Spark job in Azure HDInsight takes a long time to run. Additionally, one of the following errors might also be encoutnered:

```java
ERROR ApplicationMaster: RECEIVED SIGNAL TERM

ERROR CoarseGrainedExecutorBackend: RECEIVED SIGNAL TERM

java.lang.OutOfMemoryError: GC overhead limit exceeded


```

## Cause

Spark jobs use worker resources and when enough resources are not available, the job will be queued until the needed resources can be made available. In the meanwhile, a timeout could occur as the application waiting for resources and gets timed out.

## Solution

Three key parameters that are often adjusted to tune Spark configurations to improve application requirements are spark.executor.instances, spark.executor.cores, and spark.executor.memory. 

Depending on your Spark workload, you may determine that a non-default Spark configuration provides more optimized Spark job executions. You should perform benchmark testing with sample workloads to validate any non-default cluster configurations. Some of the common parameters that you may consider adjusting are:

  --num-executors sets the number of executors
  
  --executor-cores sets the number of cores for each executor
  
  --executor-memory controls the memory size (heap size) of each executor on Apache Hadoop YARN, and you'll need to leave some memory for execution overhead
  
1. Make sure that the cluster to be used has enough resources by verifying the applications currently running in spark cluster, using Yarn UI. Another source of information about the resources being used by the Spark Executors is the Spark Application UI. In the Spark UI, select the Executors tab to display Summary and Detail views of the configuration and resources consumed by the executors. These views can help you determine whether to change default values for Spark executors for the entire cluster, or a particular set of job executions. 

2. Following command is an example of how to change the configuration parameters for a batch application that is submitted using spark-submit:

spark-submit --class <the application class to execute> --executor-memory 3072M --executor-cores 4 –-num-executors 10 <location of application jar file> <application parameters>




