#

## Apache Spark
Apache Spark is a distributed data processing framework that enables large-scale data analytics by coordinating work across multiple processing nodes in a cluster, known in Microsoft Fabric as a _Spark pool_.
In simple terms, task are distributed across multiple computers to speed up the task. The distribution of task and collating results is automated by Spark.

## Spark Pool
A Spark pool consists of compute nodes that distribute data processing tasks. The general architecture is shown in the following diagram.

<img src="https://github.com/user-attachments/assets/30a8fc98-8825-4bfe-9569-1bb282cd3efb" width ="500"></img>

As shown in the diagram, a Spark pool contains two kinds of node:

* A head node in a Spark pool coordinates distributed processes through a driver program.
* The pool includes multiple worker nodes on which executor processes perform the actual data processing tasks.

The Spark pool uses this distributed compute architecture to access and process data in a compatible data store - such as a data lakehouse based in OneLake.

## Runtime & Environment
Spark runtime determines the version of Apache Spark, Delta Lake, Python, and other core software components that are installed. 
Additionally, within a runtime you can install and use a wide selection of code libraries for common (and sometimes very specialized) tasks

> PySpark is most commonly used for Spark processing, there's likely a specific python library to achieve your niche

Multiple environments are created to support a diverse range of data processing tasks. Each environment defines a specific runtime version as well as the libraries that must be installed to perform specific operations.

## PySpark Syntax
This is something worth looking into.

