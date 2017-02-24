# About

This is a demonstration of micro services development using spring, kafka/zookeeper. Code provides 

'DataSource, MyDataProcessor, DataSink' 


## Pre-requisites

In order to test this application in a docker environment; you must have docker and docker-compose installed. 


## Monitoring

Monitoring of Kafka queues is done through Grafana therefore, Kafka needs to be started with JMX exporter as command line argument together with Prometheus. In order to setup monitoring, following steps are needed for Dockers included with application;


## Building for Production ('prod') profile with Docker 

Since Kafka/Zookeeper are required for publisher/subscriber messaging system, a docker file is provided that already contains kafka, zookeeper, prometheus, graphana and graf_db images. To fully dockerize this application and all the services that it depends on, build with production profile with docker support as below;

	./mvnw package -Pprod docker:build


## Initialize Docker Containers

To initialize docker container run below command from root directory:

    docker-compose -f src/main/docker/app.yml up

To stop it and remove the container, run:

    docker-compose -f src/main/docker/app.yml down

## Accessibility

Kafka mertics exposed through JMX is visible here;
    
    http://<IP-ADDRESS-OF-KAFKA-BROKER>:8080/metrics

Grafana Dashboard is accessible here

	http://<IP-ADDRESS-OF-KAFKA-BROKER>:3000
	
## Troubleshooting

In some instances, you will notice failure while building because following environment variables need settings;

DOCKER_CERT_PATH=/Users/<username>/.docker/machine/certs/

DOCKER_HOST=tcp://192.168.99.100:2376

DOCKER_TLS_VERIFY=1

like;

export DOCKER_HOST=tcp://192.168.99.100:2376