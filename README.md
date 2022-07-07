# Data transformations with Python
This project is a collection of solutions in Spark _Python_ for the problems described below.

## Project Setup

This project can be setup in two ways. Each of these mechanisms support the following requirements:
* Compile (if required)
* Lint the code
* Run unit and integration tests
* Package (if required)
* Run the jobs

### Local setup in an IDE (preferred)
Setup of the project in an IDE of your choice. This is preferred as this is a setup you are most likely to be familiar and comfortable with. 

[This](README-LOCAL.md) is how to setup using an IDE.

### Using containers
In the rare cases the local setup of the project isn't feasible, this project can be setup using containers locally. This, however, maybe a bit more complex because of pre-requisites like batect, colima/docker desktop amongst others.

[This](README-CONTAINERS-WINDOWS.md) is how to setup using containers on a *Windows* machine.

[This](README-CONTAINERS-NON-WINDOWS.md) is how to setup using containers on a *Mac/Linux* machine.

These jobs are using _PySpark_ to process larger volumes of data and are supposed to run on a _Spark_ cluster (via `spark-submit`).

## Jobs

There are two applications in this repo: Word Count, and Citibike.

Currently, these exist as skeletons, and have some initial test cases which are defined but ignored.
For each application, please un-ignore the tests and implement the missing logic.

### Word Count
A NLP model is dependent on a specific input file. This job is supposed to preprocess a given text file to produce this
input file for the NLP model (feature engineering). This job will count the occurrences of a word within the given text
file (corpus). 

There is a dump of the datalake for this under `resources/word_count/words.txt` with a text file.

#### Input
Simple `*.txt` file containing text.

#### Output
A single `*.csv` file containing data similar to:
```csv
"word","count"
"a","3"
"an","5"
...
```


### Citibike (Distance Compuation)
***This problem uses data made publically available by [Citibike](https://citibikenyc.com/), a New York based bike share company.***

For analytics purposes, the BI department of a hypothetical bike share company would like to present dashboards, displaying the
distance each bike was driven. There is a `*.csv` file that contains historical data of previous bike rides. This input
file needs to be processed in multiple steps. There is a pipeline running these jobs.

![citibike pipeline](docs/citibike.png)

There is a dump of the datalake for this under `resources/citibike/citibike.csv` with historical data.

#### Ingest
Reads a `*.csv` file and transforms it to parquet format. The column names will be sanitized (whitespaces replaced).

##### Input
Historical bike ride `*.csv` file:
```csv
"tripduration","starttime","stoptime","start station id","start station name","start station latitude",...
364,"2017-07-01 00:00:00","2017-07-01 00:06:05",539,"Metropolitan Ave & Bedford Ave",40.71534825,...
...
```

##### Output
`*.parquet` files containing the same content
```csv
"tripduration","starttime","stoptime","start_station_id","start_station_name","start_station_latitude",...
364,"2017-07-01 00:00:00","2017-07-01 00:06:05",539,"Metropolitan Ave & Bedford Ave",40.71534825,...
...
```

#### Distance calculation
This job takes bike trip information and calculates the "as the crow flies" distance traveled for each trip.
It reads the previously ingested data parquet files.

Hint:
 - For distance calculation, consider using [**Harvesine formula**](https://en.wikipedia.org/wiki/Haversine_formula) as an option.  

##### Input
Historical bike ride `*.parquet` files
```csv
"tripduration",...
364,...
...
```

##### Outputs
`*.parquet` files containing historical data with distance column containing the calculated distance.
```csv
"tripduration",...,"distance"
364,...,1.34
...
```

