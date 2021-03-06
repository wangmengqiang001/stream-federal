# create cluster with several plugins which can be deployed or not optionally.

## Contents
- Create network
- deploy zookeeper, kafka, flink cluster
- deploy web-ui utilities for kafka
- undeploy all 
- deploy by docker-compose

## create network
````
./createNet.sh 
# it will create network zookeeper-kafka-net (subnet 10.1.3.0/24)
````

## deploy zookeeper, kafka, flink cluster

````
docker stack up a -c docker-compose.yml 
docker stack up b -c docker-flink.yml

````

## deploy web-ui utilities for kafka
````
docker stack up c -c docker-kafka-tools.yml
````

````console
> docker stack ls
NAME                SERVICES            ORCHESTRATOR
a                   5                   Swarm
b                   2                   Swarm
c                   2                   Swarm
````

## undeploy all
````console
> docker stack rm a b c

Removing service a_kafka
Removing service a_kafka1
Removing service a_zookeeper1
Removing service a_zookeeper2
Removing service a_zookeeper3
Removing service b_jobmanager
Removing service b_taskmanager
Removing service c_kafka-manager
Removing service c_kafka-ui
````

## deploy or undeploy by docker-compose
````console

> ./createNet.sh 
# create the network （----attachable should be added）

> docker-compose -p a -f docker-compose.yml -f docker-flink.yml -f docker-kafka-tools.yml up -d
# deploy as whole project a


> docker-compose -p a -f docker-compose.yml -f docker-flink.yml -f docker-kafka-tools.yml down
# undeploy whole project a

or 
> docker-compose -p a -f docker-compose.yml -f docker-flink.yml up
# only run zookeeper, kafka, flink

> docker-compose -p a -f docker-compose.yml -f docker-kafka-tools.yml up -d
# append kafka-ui & kafak-manager

> docker-compose -p a -f docker-compose.yml -f docker-kafka-tools.yml stop kafka-ui kafka-manager
# stop kafka-ui & kafka-manager
> docker-compose -p a -f docker-compose.yml -f docker-kafka-tools.yml rm kafka-ui kafka-manager
# rm kafka-ui & kafka-manager
````
