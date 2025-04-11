# Real Time Intelligence
Fabric's Real time Intelligence solution deal with real time data (i.e. continous stream of data in real time).

Using the Microsoft Fabric Real-Time Intelligence, you can:

* Create an eventstream to capture, transform, and ingest real-time data from various streaming sources.
* Store captured real-time data in an eventhouse, which includes one or more KQL databases.
* Query and analyze data in the eventhouse by using KQL queries, organized in a KQL queryset.
* Visualize real-time data in a real-time dashboard or by using Power BI.
* Configure alerts that use Activator to trigger automated actions.


## Ingesting and Transforming Real Time Data
_Eventstreams_ in Microsoft Fabric are used to capture, transform, and load real-time data from a wide range of streaming data sources. 
Setting up an eventstream defines a data processing engine that runs perpetually to ingest and transform real-time data. 
You tell it where to get data from, where to send it, and how to change it along the way if needed.

### Eventstream Data Sources
Eventstreams in Microsoft Fabric support a wide range of data sources, including:

* **External services**, like Azure Storage, Azure Event Hubs, Azure IoT Hubs, Apache Kafka hubs, Change Data Capture (CDC) feeds in relational database services, and others.
* **Fabric events**, such as changes to items in a Fabric workspace, data changes in OneLake data stores, and events associated with Fabric jobs.
* **Sample data**, which includes a range of samples that can help you explore real-time analytics scenarios in Microsoft Fabric.

### Eventstream Data Distination

* Eventhouse: This destination lets you ingest your real-time event data into an eventhouse, where you can use Kusto Query Language (KQL) to query and analyze the data.
* Lakehouse: This destination gives you the ability to transform your real-time events before ingesting them into your lakehouse. Real-time events convert into Delta Lake format and then store in the designated lakehouse tables.
* Derived stream: Derived stream is used to redirect the output of your eventstream to another eventstream. The derived stream represents the transformed default stream following stream processing.
* Fabric Activator: This destination lets you directly connect your real-time event data to a Fabric Activator; which is an intelligent agent that can automate actions based on values in the stream.
* Custom endpoint: With this destination, you can route your real-time events to a custom endpoint. This destination is useful when you want to direct real-time data to an external system or custom application outside Microsoft Fabric.

## Store & Query Real-Time Data
