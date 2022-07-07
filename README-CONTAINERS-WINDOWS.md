# Setup and running the project using containers on a Windows machine

## Pre-requisites

We use [`batect`](https://batect.dev/) to dockerise the tasks in this exercise. 
`batect` is a lightweight wrapper around Docker that helps to ensure tasks run consistently (across linux, mac windows).
With `batect`, the only dependencies that need to be installed are Docker and Java >=8. Every other dependency is managed inside Docker containers.
If docker desktop can't be installed then Colima could be used on Mac and Linux. 

> **For Windows, docker desktop is the only option for using container to run application
otherwise local laptop should be set up.**

Please make sure you have the following installed and can run them

* Docker Desktop
* Java (11)


You could use following instructions as guidelines to install Docker and Java.

```bash
# Install pre-requisites needed by batect 
# Please ensure Docker and java >=8 is installed 
scripts\install_choco.ps1
scripts\install.bat
```

> **Please install poetry if you would like to use lint command. Instructions to install poetry in [README-LOCAL](README-LOCAL.md) **


## List of commands

Full list of commands for Windows users is as follows:

| S.No.      | Command | Action     |
| :---:        |    :----   |          :--- |
| 1      | go.ps1 linting       | Static analysis, code style, etc. (please install poetry if you would like to use this command)  |
| 2      | go.ps1 install-with-docker-desktop       | Install the application requirements along with docker desktop   |
| 3      | go.ps1 run-local-unit-test       | Run unit tests on local machine   |
| 4      | go.ps1 run-docker-desktop-unit-test       | Run unit tests on containers using Docker Desktop   |
| 5      | go.ps1 run-local-integration-test       | Run integration tests on local machine   |
| 6     | go.ps1 run-docker-desktop-integration-test       | Run integration tests on containers using Docker Desktop   |
| 7     | go.ps1 run-local-job       | Run job on local machine   |
| 8     | go.ps1 run-docker-desktop-job       | Run job on containers using Docker Desktop   |
| 9     | go.ps1 Usage       | Display usage   |


## Jobs

### Word Count

#### Run the job using Docker Desktop on Windows

```bash
$env:JOB = wordcount 
.\go.ps1 run-docker-desktop-job 
```

### Citibike

#### Ingest
Reads a `*.csv` file and transforms it to parquet format. The column names will be sanitized (whitespaces replaced).

##### Run the job using Docker Desktop on Windows

```bash
$env:JOB = citibike_ingest
.\go.ps1 run-docker-desktop-job
```

#### Distance calculation
This job takes bike trip information and calculates the "as the crow flies" distance traveled for each trip.
It reads the previously ingested data parquet files.

Hint:
 - For distance calculation, consider using [**Harvesine formula**](https://en.wikipedia.org/wiki/Haversine_formula) as an option.  

##### Run the job using Docker Desktop on Windows

```bash
$env:JOB = citibike_distance_calculation 
.\go.ps1 run-docker-desktop-job
```
