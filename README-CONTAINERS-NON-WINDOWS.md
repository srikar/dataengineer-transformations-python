# Setup and running the project using containers on Mac/Linux

## Pre-requisites

We use [`batect`](https://batect.dev/) to dockerise the tasks in this exercise. 
`batect` is a lightweight wrapper around Docker that helps to ensure tasks run consistently (across linux, mac windows).
With `batect`, the only dependencies that need to be installed are Docker and Java >=8. Every other dependency is managed inside Docker containers.
If docker desktop can't be installed then Colima could be used on Mac and Linux. 

Please make sure you have the following installed and can run them

* Docker Desktop or Colima
* Java (11)


You could use following instructions as guidelines to install Docker or Colima and Java.

```bash
# Install pre-requisites needed by batect 
# For mac users: 
./go.sh install-with-docker-desktop
OR
./go.sh install-with-colima

# For linux users:
# Please ensure Docker and java >=8 is installed 
scripts\install_choco.ps1
scripts\install.bat

# For local laptop setup ensure that Java 11 with Spark 3.2.1 is available. More details in README-LOCAL.md
```

> **If you are using Colima, please ensure that you start Colima. For staring Colima, you could use following command:**

`./go.sh start-colima`


> **Please install poetry if you would like to use lint command. Instructions to install poetry in [README-LOCAL](README-LOCAL.md) **


## List of commands

General pattern apart from installation and starting of Colima is:

`./go.sh run-<type>-<action>`

type could be local, colima or docker-desktop

action could be unit-test, integration-test or job.

Full list of commands for Mac and Linux users is as follows: 

| S.No.      | Command | Action     |
| :---:        |    :----   |          :--- |
| 1      | ./go.sh lint       | Static analysis, code style, etc. (please install poetry if you would like to use this command)   |
| 2      | ./go.sh linting       | Static analysis, code style, etc. (please install poetry if you would like to use this command)   |
| 3      | ./go.sh install-with-docker-desktop       | Install the application requirements along with docker desktop   |
| 4      | ./go.sh install-with-colima       | Install the application requirements along with colima   |
| 5      | ./go.sh start-colima       | Start Colima   |
| 6      | ./go.sh run-local-unit-test       | Run unit tests on local machine   |
| 7      | ./go.sh run-colima-unit-test       | Run unit tests on containers using Colima   |
| 8      | ./go.sh run-docker-desktop-unit-test       | Run unit tests on containers using Docker Desktop   |
| 9      | ./go.sh run-local-integration-test       | Run integration tests on local machine   |
| 10      | ./go.sh run-colima-integration-test       | Run integration tests on containers using Colima   |
| 11     | ./go.sh run-docker-desktop-integration-test       | Run integration tests on containers using Docker Desktop   |
| 12     | ./go.sh run-local-job       | Run job on local machine   |
| 13     | ./go.sh run-colima-job       | Run job on containers using Colima   |
| 14     | ./go.sh run-docker-desktop-job       | Run job on containers using Docker Desktop   |
| 15     | ./go.sh Usage       | Display usage   |


## Jobs

### Word Count

#### Run the job using Docker Desktop on Mac or Linux

```bash
JOB=wordcount ./go.sh run-docker-desktop-job 
```

#### Run the job using Colima

```bash
JOB=wordcount ./go.sh run-colima-job 
```

### Citibike

#### Ingest

##### Run the job using Docker Desktop on Mac or Linux

```bash
JOB=citibike_ingest ./go.sh run-docker-desktop-job
```

##### Run the job using Colima

```bash
JOB=citibike_ingest ./go.sh run-colima-job
```

#### Distance calculation

##### Run the job

##### Run the job using Docker Desktop on Mac or Linux

```bash
JOB=citibike_distance_calculation ./go.sh run-docker-desktop-job
```

##### Run the job using Colima

```bash
JOB=citibike_distance_calculation ./go.sh run-colima-job
```
