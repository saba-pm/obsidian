1. Topics: a particular stream of data
	- similar to a table in a database 
	- A topic provides a destination for the storage of data. Each topic is split into one or more partitions.
	- you can have as many topics as you want
	- a topic is identified by its ==name== 
	- Topics are split in partition
	- each partition is ordered
	- each message within a partition gets an incremental ID, called  ==offset==.

2. Broker
	- a Kafka cluster composed of multiple brokers(server)
	- each broker is identified with its ID (integer)
	- each broker contains certain topic partitions
	- after connection to any broker (called a bootstrap broker), you will be connected to the entire cluster 
	- a good number to get started is 3 brokers,  but some big cluster have over 100 brokers.
	- In these examples, we choose to number brokers starting at 100 (arbitrary)

Concept of leader for a partition
 - at any time only one broker can be a leader for a given partition
 - only that leader can receive and serve data for a partition
 - the other brokers will synchronize the data
 - therefore each partition has one leader and multiple ISR (in-sync replica). 

### Kafka component interaction

  ![[Pasted image 20240204115038.png]]

**Apache ZooKeeper**

Apache ZooKeeper is a core dependency for Kafka as it provides a cluster coordination service, storing and tracking the status of brokers and consumers. ZooKeeper is also used for controller election.

**Kafka Connect**

Kafka Connect is an integration toolkit for streaming data between Kafka brokers and other systems using _Connector_ plugins. Kafka Connect provides a framework for integrating Kafka with an external data source or target, such as a database, for import or export of data using connectors. Connectors are plugins that provide the connection configuration needed.

- A _source_ connector pushes external data into Kafka.
    
- A _sink_ connector extracts data out of Kafka
    
    External data is translated and transformed into the appropriate format.
    
    You can deploy Kafka Connect with `build` configuration that automatically builds a container image with the connector plugins you require for your data connections.
    

**Kafka MirrorMaker**

Kafka MirrorMaker replicates data between two Kafka clusters, within or across data centers.

MirrorMaker takes messages from a source Kafka cluster and writes them to a target Kafka cluster.

**Kafka Bridge**

Kafka Bridge provides an API for integrating HTTP-based clients with a Kafka cluster.

**Kafka Exporter**

kafka Exporter extracts data for analysis as Prometheus metrics, primarily data relating to offsets, consumer groups, consumer lag and topics. Consumer lag is the delay between the last message written to a partition and the message currently being picked up from that partition by a consumer

### Common configuration
Some of the configuration options common to resources are described here. [Security](https://strimzi.io/docs/operators/latest/overview#security-overview_str) and [metrics collection](https://strimzi.io/docs/operators/latest/overview#metrics-overview_str) might also be adopted where applicable.

1. Bootstrap servers
	Bootstrap servers are used for host/port connection to a Kafka cluster for:

- Kafka Connect
    
- Kafka Bridge
    
- Kafka MirrorMaker producers and consumers
    

2. CPU and memory resources
	You request CPU and memory resources for components. Limits specify the maximum resources that can be consumed by a given container.

Resource requests and limits for the Topic Operator and User Operator are set in the `Kafka` resource.

3. Logging
	You define the logging level for the component. Logging can be defined directly (inline) or externally using a config map.

***Health checks***
	Healthcheck configuration introduces _liveness_ and _readiness_ probes to know when to restart a container (liveness) and when a container can accept traffic (readiness).

***JVM options***
	JVM options provide maximum and minimum memory allocation to optimize the performance of the component according to the platform it is running on.

***Pod scheduling***
	Pod schedules use _affinity/anti-affinity_ rules to determine under what circumstances a pod is scheduled onto a node.
 Operators within the Strimzi architecture
##### Cluster Operator
Strimzi uses the Cluster Operator to deploy and manage clusters. By default, when you deploy Strimzi, a single Cluster Operator replica is deployed. You can add replicas with leader election so that additional Cluster Operators are on standby in case of disruption.

The Cluster Operator manages the clusters of the following Kafka components:

- Kafka (including ZooKeeper, Entity Operator, Kafka Exporter, and Cruise Control)
    
- Kafka Connect
    
- Kafka MirrorMaker
    
- Kafka Bridge

##### Topic Operator
The Topic Operator provides a way of managing topics in a Kafka cluster through `KafkaTopic` resources.
The Topic Operator manages Kafka topics by watching for `KafkaTopic` resources that describe Kafka topics, and ensuring that they are configured properly in the Kafka cluster.

When a `KafkaTopic` is created, deleted, or changed, the Topic Operator performs the corresponding action on the Kafka topic.

You can declare a `KafkaTopic` as part of your application’s deployment and the Topic Operator manages the Kafka topic for you.

The Topic Operator operates in the following modes:

Unidirectional mode

Unidirectional mode means that the Topic Operator solely manages topics through the `KafkaTopic` resource. This mode does not require ZooKeeper and is compatible with using Strimzi in KRaft mode.

Bidirectional mode

Bidirectional mode means that the Topic Operator can reconcile changes to a `KafkaTopic` resource to and from a Kafka cluster. This means that you can update topics either through the `KafkaTopic` resource or directly in Kafka, and the Topic Operator will ensure that both sources are updated to reflect the changes. This mode requires ZooKeeper for cluster management.

The Topic Operator maintains information about each topic in a _topic store_, which is continually synchronized with updates from Kubernetes `KafkaTopic` custom resources or Kafka topics. Updates from operations applied to a local in-memory topic store are persisted to a backup topic store on 
	Manages Kafka topics
#####  User Operator.

The User Operator provides a way of managing users in a Kafka cluster through `KafkaUser` resources.

The User Operator manages Kafka users for a Kafka cluster by watching for `KafkaUser` resources that describe Kafka users, and ensuring that they are configured properly in the Kafka cluster.

When a `KafkaUser` is created, deleted, or changed, the User Operator performs the corresponding action on the Kafka user.

You can declare a `KafkaUser` resource as part of your application’s deployment and the User Operator manages the Kafka user for you. You can specify the authentication and authorization mechanism for the user. You can also configure _user quotas_ that control usage of Kafka resources to ensure, for example, that a user does not monopolize access to a broker.

When the user is created, the user credentials are created in a `Secret`. Your application needs to use the user and its credentials for authentication and to produce or consume messages.

In addition to managing credentials for authentication, the User Operator also manages authorization rules by including a description of the user’s access rights in the `KafkaUser` declaration.

![[Pasted image 20240204143001.png]]   

## Install Kafka with strimzi

1. create Kafka namespace  
```
kubectl create namespace kafka
```

2. Install strimzi operator  
Apply the Strimzi install files, including `ClusterRoles`, `ClusterRoleBindings` and some `Custom Resource Definitions (CRDs)`. The CRDs define the sachems used for the custom resources (CRs, such as Kafka, `KafkaTopic` and so on) you will be using to manage `Kafka clusters`, topics, and users.
```
kubectl create -f 'https://strimzi.io/install/latest?namespace=kafka' -n kafka
```

####  Create an Apache Kafka cluster
3. create a new Kafka custom resource to get a small persistent Apache Kafka Cluster with one node for Apache Zookeeper and Apache Kafka:
```
kubectl apply -f https://strimzi.io/examples/latest/kafka/kafka-persistent-single.yaml -n kafka 
```
 simple example:
 ```
apiVersion: kafka.strimzi.io/v1beta2
kind: Kafka
metadata:
  name: my-cluster
spec:
  kafka:
    version: 3.6.1
    replicas: 1
    listeners:
      - name: plain
        port: 9092
        type: internal
        tls: false
      - name: tls
        port: 9093
        type: internal
        tls: true
    config:
      offsets.topic.replication.factor: 1
      transaction.state.log.replication.factor: 1
      transaction.state.log.min.isr: 1
      default.replication.factor: 1
      min.insync.replicas: 1
      inter.broker.protocol.version: "3.6"
    storage:
      type: jbod
      volumes:
      - id: 0
        type: persistent-claim
        size: 100Gi
        deleteClaim: false
  zookeeper:
    replicas: 1
    storage:
      type: persistent-claim
      size: 100Gi
      deleteClaim: false
  entityOperator:
    topicOperator: {}
    userOperator: {}
```

if you want to define resource, you need to define like these:
```
apiVersion: kafka.strimzi.io/v1beta2
kind: Kafka
metadata:
  name: my-cluster

spec:

	kafka:
		listeners:
			- name: tls
			  port: 9093
			  type: internal
               tls: true
               authentication:
               type: tls
			- name: external1
			  port: 9094
              type: route
               tls: true
               authentication:
               type: tls

# ...
		storage:
			type: persistent-claim
			size: 10000Gi

# ...
		rack:
			topologyKey: topology.kubernetes.io/zone
		config:
			replica.selector.class: org.apache.kafka.common.replica.RackAwareReplicaSelector

```
