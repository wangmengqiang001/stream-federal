# create cluster with several plugins which can be deployed or not optionally.

## Contents
- Create network
- deploy zookeeper, kafka, flink cluster
- deploy web-ui utilities for kafka
- undeploy all 

## create network
````
./createNet.sh 
# it will create network zookeeper-kafka-net (subnet 10.1.3.0/24)
````

## deploy zookeeper, kafka, flink cluster

````
docker stack up a -c docker-compose.yml
````

## deploy web-ui utilities for kafka
````
docker stack up b -c docker-kafka-tools.yml
````

````console
> docker stack ls
NAME                SERVICES            ORCHESTRATOR
a                   7                   Swarm
b                   2                   Swarm
````

## undeploy all
````console
> docker stack rm a b

Removing service a_jobmanager
Removing service a_kafka
Removing service a_kafka1
Removing service a_taskmanager
Removing service a_zookeeper1
Removing service a_zookeeper2
Removing service a_zookeeper3
Removing service b_kafka-manager
Removing service b_kafka-ui
````
