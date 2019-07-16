---
title: Azure HDInsight Solutions | Apache Spark | Resource Allocation
description: How resource alloation works in HDInsight Spark Solutions
services: hdinsight
author: confusionblinds
ms.author: deeptivu
ms.service: hdinsight
ms.custom: troubleshooting
ms.topic: conceptual
ms.date: 10/30/2018
---
# Azure HDInsight Solutions | Spark | resource allocation

## Scenario: Spark activity running in Azure Data Factory fails with IllegalArgumentException

## Issue

Spark job in Azure HDInsight takes a long time to run. Additionally, one of the following errors might also be encoutnered:

```java

```

## Cause

Spark jobs use worker resources and when enough resources are not available, the job will be queued until the needed resources can be made available. In the meanwhile, a timeout could occur as the application waiting for resources and gets timed out.

## Solution

Three key parameters that are often adjusted to tune Spark configurations to improve application requirements are spark.executor.instances, spark.executor.cores, and spark.executor.memory. 

Depending on your Spark workload, you may determine that a non-default Spark configuration provides more optimized Spark job executions. You should perform benchmark testing with sample workloads to validate any non-default cluster configurations. Some of the common parameters that you may consider adjusting are:

  --num-executors sets the number of executors
  
  --executor-cores sets the number of cores for each executor
  
  --executor-memory controls the memory size (heap size) of each executor on Apache Hadoop YARN, and you'll need to leave some memory for execution overhead
  
When configuring a spark application like below, make sure that the parameters value is within the available resources at the time. Otherwise, the job will wait until the resources are available.
