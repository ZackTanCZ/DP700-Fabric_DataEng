# Two important part of Real Time Analytics

## Eventhouse
* Database optimise for large amount of real time data
* Uses the KQL to query KQL Database
* Both KQL and SQL can be used; KQL is preferred as it is optimised


## KQL 
* Filter Columns - `project` keyword

KQL
> Automotive  
> | project trip_id, vendor_id, pickup_datetime, fare_amount

SQL 
> SELECT trip_id, vendor_id, pickup_datetime, fare_amount  
> FROM Automotive

* Filter Rows - `where` keyword

KQL
> Automotive  
> | where getmonth(pickup_datetime) == getmonth(now())  
> and getyear(pickup_datetime) == getyear(now())  
> | project trip_id, vendor_id, pickup_datetime, fare_amount

SQL
> SELECT trip_id, vendor_id, pickup_datetime, fare_amount  
> FROM Automotive  
> WHERE MONTH(pickup_datetime) == MONTH(now()) AND  
> YEAR(pickup_datetime) == YEAR(now())

KQL
> Automotive  
> | where pickup_datetime > ago(30min)  
> | project trip_id, vendor_id, pickup_datetime, fare_amount

```
Find trip_id, vendor_id, pickup_datetime, fare_amount
where pickup_datetime is more than 30mins ago
```

KQL
> Automotive  
> | where ingestion_time() > ago(1h)  
> | project trip_id, vendor_id, pickup_datetime, fare_amount

```
Find trip_id, vendor_id, pickup_datetime, fare_amount
where the time when data was ingested into the KQL database is more than 1 hour ago
```

KQL
> Automotive
> | where ingestion_time() > ago(1d)
> | summarize average_fare = avg(fare_amount) by vendor_id, pickup_hour = hourofday(pickup_datetime)
> | project pickup_hour, vendor_id, average_fare
> | sort by pickup_hour

```
Find  vendor_id, pickup_hour, the average fare_amount of each vender from automotive table
where the time when data was ingested into the KQL database is more than 1 day ago
order by pickup_hour
```

## Eventstream




###
