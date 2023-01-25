## Q1
```
docker build --help
```

## Q2
Create docker image with this dockerfile

```
# base Docker image that we will build on
FROM python:3.9.1
# set up the working directory inside the container
WORKDIR /app
# define what to do first when the container runs
# in this example, we will go to bash
CMD ["/bin/bash"]
```

Then run 
```
docker build -t dummy:v001 .
docker run -it dummy:v001
```

Once inside the bash, run
```
pip list
```

## Q3
```
select count(*) from yellow_taxi_trips
where date(lpep_pickup_datetime) = '2019-01-15'
and date(lpep_dropoff_datetime) = '2019-01-15'
```

## Q4
```
select * from yellow_taxi_trips
where trip_distance IN (
	select max(trip_distance)
	from yellow_taxi_trips
)
```

## Q5
```
select passenger_count, count(*) from yellow_taxi_trips
where 
date(lpep_pickup_datetime) = '2019-01-01'
-- and 
-- date(lpep_dropoff_datetime) = '2019-01-01'
group by 1
```

## Q6
```
select dropoff_zone, sum(tip_amount)
from
(
	select yellow_taxi_trips.*, a."Zone" as pickup_zone,
	b."Zone" as dropoff_zone
	from yellow_taxi_trips
	left join taxi_zone as a
	on yellow_taxi_trips."PULocationID" = a."LocationID"
	left join taxi_zone as b
	on yellow_taxi_trips."DOLocationID" = b."LocationID"
	where a."Zone" = 'Astoria'
) as b
group by 1
order by 2 desc
```
