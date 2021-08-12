# docker-apache-airflow
Apache Airflow using Docker Compose

## Usage

### Docker Compose

Im using the [taskfile](https://taskfile.dev) build tool to simplify usage. But running without taskfile,

To build the dependency image:

```
docker-compose -f deps.docker-compose.yml build
```

Once the `airflow-dependencies:1.10.14` image is built, you can build the rest and start the containers:

```
docker-compose up --build -d
```

### Taskfile

Im using the [taskfile](https://taskfile.dev) build tool to simplify usage.

To install on a mac:

```
brew install go-task/tap/go-task
```

To install on linux: 

```
sh -c "$(curl --location https://taskfile.dev/install.sh)" -- -d -b /usr/local/bin
```

Then for help run:

```
task

task: Available tasks for this project:
* build: 	Builds airflow
* clean: 	Runs docker system prune -f --all
* default: 	Runs the help task
* down: 	Stops containers
* help: 	Runs the list tasks
* logs: 	Runs docker-compose logs -f
* run: 		Runs docker-compose up -d
* verify: 	Verify if docker is running
```

To build and start:

```
task build
task run
```

## Endpoints

The default username is `admin` and the password is `password` but configurable on the environment variable `AIRFLOW_ADMIN_PASSWORD`.

Airflow:
- http://localhost:8080

Flower:
- http://localhost:5556

## Screenshots

Airflow UI:

![image](https://user-images.githubusercontent.com/567298/129044818-c0db478e-41c1-4bb4-bf82-c6821f2bbda3.png)

Graph View:

![image](https://user-images.githubusercontent.com/567298/129044904-82f2586e-7a6f-48f0-beae-bab1d002ae26.png)

Flower Dashboard:

![image](https://user-images.githubusercontent.com/567298/129045052-be4b5670-09b5-419c-a590-83a1c5da0435.png)

Detail about the worker:

![image](https://user-images.githubusercontent.com/567298/129045405-2fe465cb-7ffe-4d42-ad83-7764e31e9aeb.png)


Executed Tasks:

![image](https://user-images.githubusercontent.com/567298/129045257-1420898c-a7d4-4348-8f61-5610ec5c875c.png)

Broker:

![image](https://user-images.githubusercontent.com/567298/129045321-7202758e-b8a9-4116-ba02-bb33c32f821c.png)


## Resources

- [Airflow Executor: Celery](https://airflow.apache.org/docs/apache-airflow/1.10.6/howto/executor/use-celery.html)
- [Flower: Authentication](https://airflow.apache.org/docs/apache-airflow/stable/security/flower.html)
- [Github/Airflow: Example docker-compose.yml](https://github.com/apache/airflow/blob/main/docs/apache-airflow/start/docker-compose.yaml)
- [Blog: Deploy Airflow in Multiple Containers](https://towardsdatascience.com/deploy-apache-airflow-in-multiple-docker-containers-7f17b8b3de58)
- [Blog: Run Airflow in Docker](https://betterprogramming.pub/how-to-start-running-apache-airflow-in-docker-6567d8165653)

