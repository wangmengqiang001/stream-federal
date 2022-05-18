# stream-federal
deploy clusters of zooker, kafka, flink as a federal via docker-compose, swarm, k8s 

## Contents:
- deploy zookeeper cluser
- deploy all in one

## deploy zookeeper cluster
- docker-compose

````
docker-compose -f docker-zk.yml up
````
- docker swarm
````
docker stack up a -c docker-zk.yml
````

## deploy all in one
It includes 3 zookeeper nodes, 2 kafka nodes, 1+2 flink node, and two web utilities for Kafka: kafka-ui, kafka manager utilities.
- docker-compose
````console
# run by default name and yml file
docker-compose up

# run and specify the yml file and service name
docker-compose -f docker-compose.yml -p a up

````

- docker swarm
````
docker stack up all -c docker-compose.yml
````
