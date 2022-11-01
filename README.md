# Fullstack ML

## Introduction

Includes MLflow On-Premise Deployment using Docker Compose. Original repository is 
[sachua/mlflow-docker-compose](https://github.com/sachua/mlflow-docker-compose.git). The original repository has been modified to create 
images based on the last version of Minio and MLflow version 1.28.0 (compatible with PyCaret). The version of MySQL being used is 8.0.30. At the time this 
file was written, the latest available version of PyCaret is 2.3.10 and the release of MinIO is 2022-10-29T06-21-33Z. Particular effort was placed on 
making the stack compatible with the use of PyCaret as well. 

MinIO S3 is used as the artifact store and MySQL server is used as the backend store.

The stack is composed of 3 docker containers:

* MLflow server
* MinIO object storage server
* MySQL database server

A fourth container based on the [minio/mc](https://github.com/minio/mc) image is used to automatically create the mlflow bucket on MinIO S3. Just to make 
it clear, MinIO Client (mc) provides an alternative to UNIX commands like ls, cat, cp, mirror, diff, find etc. by supporting filesystems and Amazon S3 compatible cloud storage service 
(AWS Signature v2 and v4).

## How to run

1. Clone (download) this repository

    ```bash
    git clone https://github.com/ltoscano/fullstackml-docker-compose.git
    ```

2. `cd` into the `fullstackml-docker-compose` directory

3. Build and run the containers with `docker-compose`

    ```bash
    docker-compose up -d --build
    ```

4. Access MLflow UI with http://localhost:5050

5. Access MinIO UI with http://localhost:9000

Notes:

- Docker Compose allows you to access environment variables from the compose file `docker-compose.yml`. All variables (usernames, passwords, db names, access 
keys) used in the compose file are declared in the hidden file `.env`.

- Often the TCP/5000 port used by the MLflow UI is also (ab)used by other applications. For this reason, I mapped this port to TCP/5050 on the host machine. 
Anyway, the port mapping can be easily changed by editing the compose file.
