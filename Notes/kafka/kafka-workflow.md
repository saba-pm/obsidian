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

1. **Apache ZooKeeper**

	Apache ZooKeeper is a core dependency for Kafka as it provides a cluster coordination service, storing and tracking the status of brokers and consumers. ZooKeeper is also used for controller election.

2. **Kafka Connect**

	Kafka Connect is an integration toolkit for streaming data between Kafka brokers and other systems using _Connector_ plugins. Kafka Connect provides a framework for integrating Kafka with an external data source or target, such as a database, for import or export of data using connectors. Connectors are plugins that provide the connection configuration needed.
	
	- A _source_ connector pushes external data into Kafka.
	    
	- A _sink_ connector extracts data out of Kafka
	    
	    External data is translated and transformed into the appropriate format.
	    
	    You can deploy Kafka Connect with `build` configuration that automatically builds a container image with the connector plugins you require for your data connections.
	    

3. **Kafka MirrorMaker**

	Kafka MirrorMaker replicates data between two Kafka clusters, within or across data centers.
	
	MirrorMaker takes messages from a source Kafka cluster and writes them to a target Kafka cluster.
	
	**Kafka Bridge**
	
	Kafka Bridge provides an API for integrating HTTP-based clients with a Kafka cluster.

4. **Kafka Exporter**

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


## Operator deployment best practices

Installing multiple Strimzi operators in the same Kubernetes cluster, especially different versions, can lead to resource conflicts and unpredictable behavior due to their concurrent management of resources. Even with different namespaces, issues can arise because some resources like Custom Resource Definitions (CRDs) and roles have cluster-wide scope. Compatibility issues may also occur between different operator versions and Kafka clusters.

To avoid these problems, it's recommended to:

1. Install the Strimzi operator in a separate namespace from the Kafka cluster and its components.
2. Use a single Strimzi operator for all Kafka instances within a cluster.
3. Regularly update the Strimzi operator and Kafka to the latest versions.

These practices ensure stable management of Kafka instances and allow you to utilize the latest features of Strimzi.


### Deploying strimzi steps:


1. [Deploy the Cluster Operator](https://strimzi.io/docs/operators/latest/deploying#cluster-operator-str)
    
2. Use the Cluster Operator to deploy the following:
    
    1. [Kafka cluster](https://strimzi.io/docs/operators/latest/deploying#kafka-cluster-str)
        
    2. [Topic Operator](https://strimzi.io/docs/operators/latest/deploying#deploying-the-topic-operator-using-the-cluster-operator-str)
        
    3. [User Operator](https://strimzi.io/docs/operators/latest/deploying#deploying-the-user-operator-using-the-cluster-operator-str)
        
    
3. Optionally, deploy the following Kafka components according to your requirements:
    
    - [Kafka Connect](https://strimzi.io/docs/operators/latest/deploying#kafka-connect-str)
        
    - [Kafka MirrorMaker](https://strimzi.io/docs/operators/latest/deploying#kafka-mirror-maker-str)
        
    - [Kafka Bridge](https://strimzi.io/docs/operators/latest/deploying#kafka-bridge-str)

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

#### Create an Apache Kafka in cluster
1. create a new Kafka custom resource to get a small persistent Apache Kafka Cluster with one node for Apache Zookeeper and Apache Kafka:
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

Use internal Kafka cluster:
Configures an internal listener to expose Kafka using a per-broker `ClusterIP` type `Service`.

The listener does not use a headless service and its DNS names to route traffic to Kafka brokers. You can use this type of listener to expose a Kafka cluster when using the headless service is unsuitable. You might use it with a custom access mechanism, such as one that uses a specific Ingress controller or the Kubernetes Gateway API.

A new `ClusterIP` service is created for each Kafka broker pod. The service is assigned a `ClusterIP` address to serve as a Kafka _bootstrap_ address with a per-broker port number. For example, you can configure the listener to expose a Kafka cluster over a Nginx Ingress Controller with TCP port configuration.

```
spec:

	kafka:
		listeners:
			
			- name: clusterip
			
			type: cluster-ip
			
			tls: false
			
			port: 9096
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

if you want balance utilization Kafka cluster, you need to use KafkaRebalance like this:
```
apiVersion: kafka.strimzi.io/v1beta2 # The version of the Kafka CRD API.
kind: KafkaRebalance # The type of Kubernetes resource, in this case, a KafkaRebalance.
metadata:
  name: optimized-rebalance # The name of this KafkaRebalance resource.
  labels:
    strimzi.io/cluster: production-cluster # Label to associate this rebalance with the Kafka cluster named 'production-cluster'.
spec:
  goals: # List of goals that the rebalance process should optimize for.
    - CpuCapacityGoal # Ensure that CPU usage is balanced across brokers.
    - DiskCapacityGoal # Balance disk usage across brokers to avoid storage issues.
    - NetworkInboundCapacityGoal # Distribute inbound network traffic evenly.
    - NetworkOutboundCapacityGoal # Distribute outbound network traffic evenly.
    - ReplicaCapacityGoal # Balance the number of replicas across brokers.
    - LeaderReplicaBalanceGoal # Ensure an even distribution of leader replicas to spread the leadership load.
    - TopicReplicaDistributionGoal # Distribute topic replicas evenly across brokers.
    - MinTopicLeadersPerBrokerGoal # Ensure a minimum number of topic leaders per broker to spread the load.
    - NetworkInboundUsageDistributionGoal # Optimize inbound network usage distribution.
    - NetworkOutboundUsageDistributionGoal # Optimize outbound network usage distribution.
    - DiskUsageDistributionGoal # Ensure even disk usage across brokers to prevent hotspots.

 
```

### Explanation

1. **apiVersion**: Specifies the version of the Strimzi Kafka CRD API being used. In this case, it's `v1beta2`.
2. **kind**: Defines the type of the Kubernetes resource, which is `KafkaRebalance` in this example.
3. **metadata**:
    - **name**: The name of the KafkaRebalance resource. This is how you will refer to this specific rebalance operation, here named `optimized-rebalance`.
    - **labels**: Labels are key-value pairs used to organize and select resources. Here, the label `strimzi.io/cluster: production-cluster` associates this rebalance resource with the Kafka cluster named `production-cluster`.
4. **spec**:
    - **goals**: A list of goals that the rebalance process should aim to optimize. Each goal represents a specific balancing aspect for the Kafka cluster:
        - **CpuCapacityGoal**: Balances the CPU usage across all brokers to ensure no single broker is overloaded.
        - **DiskCapacityGoal**: Balances disk usage to avoid any broker running out of storage.
        - **NetworkInboundCapacityGoal**: Distributes inbound network traffic evenly to prevent any broker from becoming a bottleneck.
        - **NetworkOutboundCapacityGoal**: Distributes outbound network traffic evenly to prevent network congestion.
        - **ReplicaCapacityGoal**: Ensures an even distribution of replicas to maintain high availability and reliability.
        - **LeaderReplicaBalanceGoal**: Balances the distribution of leader replicas to spread leadership responsibilities evenly.
        - **TopicReplicaDistributionGoal**: Distributes topic replicas evenly to avoid uneven load distribution.
        - **MinTopicLeadersPerBrokerGoal**: Ensures each broker has a minimum number of topic leaders, helping to spread the load.
        - **NetworkInboundUsageDistributionGoal**: Optimizes the distribution of inbound network usage.
        - **NetworkOutboundUsageDistributionGoal**: Optimizes the distribution of outbound network usage.
        - **DiskUsageDistributionGoal**: Ensures disk usage is evenly spread across brokers to avoid hotspots.

Create kafaka topic 
```
apiVersion: kafka.strimzi.io/v1beta1 # The version of the KafkaTopic CRD API.
kind: KafkaTopic # The type of Kubernetes resource, in this case, a KafkaTopic.
metadata:
  name: my-topic # The name of this KafkaTopic resource.
  labels:
    strimzi.io/cluster: my-cluster # Label to associate this topic with the Kafka cluster named 'my-cluster'.
spec:
  partitions: 1 # The number of partitions for this topic.
  replicas: 3 # The number of replicas for this topic, ensuring high availability.
  config:
    min.insync.replicas: 2 # The minimum number of in-sync replicas required for acks=all.

```

- **partitions**: `1`
    - Specifies the number of partitions for this topic. Partitions allow Kafka to parallelize data processing and load balancing.
- **replicas**: `3`
    - Specifies the number of replicas for this topic. Replication ensures high availability and fault tolerance by keeping multiple copies of the data across different brokers.
- **config**:
    - **min.insync.replicas**: `2`
        - Configures the minimum number of in-sync replicas (ISR) required for acks=all. This setting ensures that at least two replicas must acknowledge a write for it to be considered successful, providing a balance between reliability and availability.


Create highly availability for all partitions:
 ```
 apiVersion: kafka.strimzi.io/v1beta1 # The version of the KafkaTopic CRD API.
kind: KafkaTopic # The type of Kubernetes resource, in this case, a KafkaTopic.
metadata:
  name: my-topic # The name of this KafkaTopic resource.
  labels:
    strimzi.io/cluster: my-cluster # Label to associate this topic with the Kafka cluster named 'my-cluster'.
spec:
  partitions: 3 # The number of partitions for this topic.
  replicas: 3 # The number of replicas for this topic, ensuring high availability.
  config:
    min.insync.replicas: 2 # The minimum number of in-sync replicas required for acks=all.
    broker.rack: rack1,rack2,rack3 # Distribute partitions across different racks (brokers).

```
1. - **config**:
        - **min.insync.replicas**: `2`
            - Configures the minimum number of in-sync replicas (ISR) required for acks=all. This setting ensures that at least two replicas must acknowledge a write for it to be considered successful, providing a balance between reliability and availability.
        - **broker.rack**: `rack1,rack2,rack3`
            - Distributes partitions across different racks (brokers). By specifying `rack1`, `rack2`, and `rack3`, you ensure that Kafka will automatically distribute partitions across these brokers, balancing the load and ensuring redundancy.

This configuration helps in achieving a balanced distribution of partitions across all brokers in the cluster, ensuring high availability and efficient use of resources.

Broker highly availability:
```
rack:  # This is a custom label indicating a rack or zone for the Kafka broker.
  topologyKey: topology.kubernetes.io/zone  # This specifies that the rack/zone is determined by the Kubernetes node label for the zone.

```
