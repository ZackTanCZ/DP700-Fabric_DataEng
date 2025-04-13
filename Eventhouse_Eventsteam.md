# Two important part of Real Time Analytics

## Eventstream

## Eventhouse
* Database optimise for large amount of real time data
* Uses the KQL to query KQL Database
* Both KQL and SQL can be used; KQL is preferred as it is optimised

### KQL 
* Filter Columns - `project` keyword

KQL
> Automotive  
> | project trip_id, vendor_id, pickup_datetime, fare_amount

SQL 
> SELECT trip_id, vendor_id, pickup_datetime, fare_amount  
> FROM Automotive

* Filter Rows - `where` keyword

KQL
```
Automotive  
| where getmonth(pickup_datetime) == getmonth(now())  
and getyear(pickup_datetime) == getyear(now())  
| project trip_id, vendor_id, pickup_datetime, fare_amount
```

SQL
```
SELECT trip_id, vendor_id, pickup_datetime, fare_amount  
FROM Automotive  
WHERE MONTH(pickup_datetime) == MONTH(now()) AND  
YEAR(pickup_datetime) == YEAR(now())
```
KQL
```
Automotive  
| where pickup_datetime > ago(30min)  
| project trip_id, vendor_id, pickup_datetime, fare_amount
```

> Find trip_id, vendor_id, pickup_datetime, fare_amount  
> where pickup_datetime is more than 30mins ago

KQL
```
Automotive  
| where ingestion_time() > ago(1h)  
| project trip_id, vendor_id, pickup_datetime, fare_amount
```
> Find trip_id, vendor_id, pickup_datetime, fare_amount  
> where the time when data was ingested into the KQL database is more than 1 hour ago

KQL
```
Automotive
| where ingestion_time() > ago(1d)
| summarize average_fare = avg(fare_amount) by vendor_id, pickup_hour = hourofday(pickup_datetime)
| project pickup_hour, vendor_id, average_fare
| sort by pickup_hour
```
> Find  vendor_id, pickup_hour, the average fare_amount of each vender from automotive table
> where the time when data was ingested into the KQL database is more than 1 day ago
> order by pickup_hour

### Materialized Views
A materialized view is a summary of data from a source table or another materialized view. The view encapsulates a summarize statement.  
Materialized views are listed in the Materialized views folder for the KQL database where you defined them in the eventhouse page.

Materialized View of the number of trips by vendor_id and pickup_date
```
.create materialized-view TripsByVendor on table Automotive
{
    Automotive
    | summarize trips = count() by vendor_id, pickup_date = format_datetime(pickup_datetime, "yyyy-MM-dd")
}
```

Creating the above materializaed view doesn't populate with exisiting data  
To do so, use an asynchronous operation to create the materialized view with the **backfill** option
```
.create async materialized-view with (backfill=true)
TripsByVendor on table Automotive
{
    Automotive
    | summarize trips = count() by vendor_id, pickup_date = format_datetime(pickup_datetime, "yyyy-MM-dd")
}
```
Materialized View can be queried like a table
```
TripsByVendor
| project pickup_date, vendor_id, trips
| sort by pickup_date desc
```

### Stored Function
