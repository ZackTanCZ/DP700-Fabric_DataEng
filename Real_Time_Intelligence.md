# Real Time Intelligence
Fabric's Real time Intelligence solution deal with real time data (i.e. continous stream of data in real time).

<img src="https://github.com/user-attachments/assets/00a89210-eb7e-490b-8c6b-a6af3e35939f" width="500"></img>

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
Eventhouses stores real-time data, often ingested by an eventstream and loaded into tables for further processing and analysis.

Within an eventhouse, you can create:

* KQL databases: real-time optimized data stores that host a collection of tables, stored functions, materialized views, and shortcuts.
* KQL querysets: Collections of KQL queries that you can use to work with data in KQL database tables. A KQL queryset supports queries written using Kusto Query Language (KQL) and a subset of the Transact-SQL language.

## Querying Data
[**Kusto Query Language (KQL)**](https://learn.microsoft.com/en-us/kusto/query/?view=microsoft-fabric) is used to write queries in Azure Data Explorer, Azure Monitor Log Analytics, Microsoft Sentinel, and Microsoft Fabric to query from a table in a KQL database. KQL is a read-only request to process data and return results. KQL queries are made of one or more query statements.

## Automate Actions
Activator is a technology in Microsoft Fabric that enables automated processing of events that trigger actions.

### Activator Core Concept
Activator operates based on four core concepts: Events, *Objects, Properties, and Rules.

* Events - Each record in a stream of data represents an event that has occurred at a specific point in time.
* Objects - The data in an event record can be used to represent an object, such as a sales order, a sensor, or some other business entity.
* Properties - The fields in the event data can be mapped to properties of the business object, representing some aspect of its state. For example, a total_amount field might represent a sales order total, or a temperature field might represent the temperature measured by an environmental sensor.
* Rules - The key to automating actions based on events is to define rules that set conditions under which an action is triggered based on the property values of objects referenced in events. For example, you might define a rule that sends an email to a maintenance manager if the temperature measured by a sensor exceeds a specific threshold.

