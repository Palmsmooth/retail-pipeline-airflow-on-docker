# Data Engineering Project: Retail Pipeline Airflow On Docker
Follow this instruction: [Running Airflow in Docker](https://airflow.apache.org/docs/apache-airflow/stable/start/docker.html)
## Fetching docker-compose.yaml
To deploy Airflow on Docker Compose, you should fetch docker-compose.yaml.
```sh
curl -LfO 'https://airflow.apache.org/docs/apache-airflow/3.1.5/docker-compose.yaml'
```
## Initializing Environment
Before starting Airflow for the first time, you need to prepare your environment, i.e. create the necessary files, directories and initialize the database.
### Setting the right Airflow user
On Linux, the quick-start needs to know your host user id and needs to have group id set to 0. Otherwise the files created in dags, logs, config and plugins will be created with root user ownership. You have to make sure to configure them for the docker-compose:
```sh
mkdir -p ./dags ./logs ./plugins ./config
echo -e "AIRFLOW_UID=$(id -u)" > .env
```
You can also build the new container image with specified requirements
```sh
docker-compose build
```

First initialization of Airflow
```sh
docker-compose up airflow-init
```

Then, after initialization, start all containers:
```sh
docker-compose up -d
```

To stop containers
```sh
docker-compose down
```

Important: In the dag file in `dags/`, do not forget to apply database credentials and do not commit passwords or credential to git.

### Keeping credentials in Environment Variables
You can keep credentials in `.env` files. Then those variables will be set in container by `docker-compose.yml` in `environment:` section.

The example of `.env` file:
```sh
AIRFLOW_UID=
AIRFLOW_GID=
MYSQL_HOST=
MYSQL_PORT=
MYSQL_USER=
MYSQL_PASSWORD=
MYSQL_DB=
MYSQL_CHARSET=
```

## Airflow UI
<img src="image\airflow.png" width="100%" height="40%">
<img src="image\Retail_pipeline.png" width="100%" height="40%">
<img src="image\success.png" width="100%" height="40%">

## result
<img src="image\data.png" width="%" height="40%">
