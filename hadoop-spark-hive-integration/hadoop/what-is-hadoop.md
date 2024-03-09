---
description: Please enjoy,  just simple description 👌.
---

# 🤖 What is Hadoop?

## 👀 Introduction

`Hadoop (the full proper name is ApacheTM Hadoop®)` is an open-source framework that was created to make it easier to work with big data. It provides a method to access data that is distributed among multiple clustered computers, process the data, and manage resources across the computing and network resources that are involved. “Hadoop” commonly refers to the core technology that consists of the four main components described below, but is also frequently used in reference to the entire ecosystem of supporting technologies and applications.

“Hadoop” also is often used interchangeably with “big data,” but it shouldn’t be. Hadoop is a framework for working with big data. It is part of the big data ecosystem, which consists of much more than Hadoop itself.

Hadoop is a distributed framework that makes it easier to process large data sets that reside in clusters of computers. Because it is a framework, Hadoop is not a single technology or product. Instead, Hadoop is made up of four core modules that are supported by a large ecosystem of supporting technologies and products.&#x20;

The modules are:

* **Hadoop Distributed File System (HDFSTM) –**Provides access to application data. Hadoop can also work with other file systems, including FTP, Amazon S3 and Windows Azure Storage Blobs (WASB), among others.
* **Hadoop YARN –** Provides the framework to schedule jobs and manage resources across the cluster that holds the data
* **Hadoop MapReduce –** A YARN-based parallel processing system for large data sets.
* **Hadoop Common –** A set of utilities that supports the three other core modules.

&#x20;Some of the well-known [Hadoop ecosystem](https://www.bmc.com/blogs/hadoop-ecosystem/) components include Oozie, Spark, Sqoop, Hive and Pig.

### What Hadoop isn’t

In this tutorial for beginners, it’s helpful to understand what Hadoop is by knowing what it is not.

* **Hadoop is not** “big data” – the terms are sometimes used interchangeably, but they shouldn’t be. Hadoop is a framework for processing big data.
* **Hadoop is not** an operating system (OS) or packaged software application.
* **Hadoop is not** a brand name. It is an open source project, although “Hadoop” may be used as part of registered brand names.

### What’s with the name?

**Hadoop was originally developed by Doug Cutting and Mike Cafarella**. According to lore, Cutting named the software after his son’s toy elephant. An image of an elephant remains the symbol for Hadoop.

### Core elements of Hadoop

There are four basic elements to Hadoop: HDFS; MapReduce; YARN; Common.

### HDFS

Hadoop works across clusters of commodity servers. Therefore there needs to be a way to coordinate activity across the hardware. Hadoop can work with any distributed file system, however the Hadoop Distributed File System is the primary means for doing so and is the heart of Hadoop technology. HDFS manages how data files are divided and stored across the cluster. Data is divided into blocks, and each server in the cluster contains data from different blocks. There is also some built-in redundancy.

### YARN

It would be nice if **YARN** could be thought of as the string that holds everything together, but in an environment where terms like Oozie, tuple and Sqoop are common, of course it’s not that simple. YARN is an acronym for Yet Another Resource Negotiator. As the full name implies, YARN helps manage resources across the cluster environment. It breaks up resource management, job scheduling, and job management tasks into separate daemons. Key elements include the **ResourceManager (RM)**, the **NodeManager (NM)** and the ApplicationMaster (AM).

Think of the ResourceManager as the final authority for assigning resources for all the applications in the system. The NodeManagers are agents that manage resources (e.g. CPU, memory, network, etc.) on each machine. NodeManagers report to the ResourceManager. ApplicationMaster serves as a library that sits between the two. It negotiates resources with ResourceManager and works with one or more NodeManagers to execute tasks for which resources were allocated.

### MapReduce

**MapReduce** provides a method for parallel processing on distributed servers. Before processing data, MapReduce converts that large blocks into smaller data sets called **tuples**. Tuples, in turn, can be organized and processed according to their key-value pairs. When MapReduce processing is complete, HDFS takes over and manages storage and distribution for the output. The shorthand version of MapReduce is that it breaks big data blocks into smaller chunks that are easier to work with.

The “Map” in MapReduce refers to the **Map Tasks** function. Map Tasks is the process of formatting data into key-value pairs and assigning them to nodes for the “Reduce” function, which is executed by **Reduce Tasks**, where data is reduced to tuples. Both Map Tasks and Reduce Tasks use **worker nodes** to carry out their functions.

**JobTracker** is a component of the MapReduce engine that manages how client applications submit MapReduce jobs. It distributes work to **TaskTracker** nodes. TaskTracker attempts to assign processing as close to where the data resides as possible.

Note that MapReduce is not the only way to manage parallel processing in the Hadoop environment.

### Common

**Common**, which is also known as **Hadoop Core**, is a set of utilities that support the other Hadoop components. Common is intended to give the Hadoop framework ways to manage typical (common) hardware failures.

{% hint style="info" %}
Read more articles :

* [BMC Blogs - Hadoop Tutorial for Beginners: Hadoop Basics](https://www.bmc.com/blogs/hadoop-introduction/)
{% endhint %}
