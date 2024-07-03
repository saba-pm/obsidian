```
apiVersion: kafka.strimzi.io/v1beta2 # The version of the Kafka CRD API.
kind: Kafka # The type of Kubernetes resource, in this case, a Kafka cluster.
metadata:
  name: cluster-name # The name of this Kafka cluster resource.
  namespace: kafka-connect # The namespace where the Strimzi operator is installed.
spec:
  kafka:
    replicas: 3 
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
      auto.create.topics.enable: false
      log.message.format.version: "2.3"
      log.retention.bytes: 1073741824
      log.retention.hours: 1
      log.retention.check.interval.ms: 300000
      offsets.topic.replication.factor: 3
      transaction.state.log.min.isr: 2
      transaction.state.log.replication.factor: 3
    livenessProbe:
      initialDelaySeconds: 15
      timeoutSeconds: 5
    readinessProbe:
      initialDelaySeconds: 15
      timeoutSeconds: 5
    storage:
      type: persistent-claim # Persistent storage using PVCs.
      size: 100Gi # Size of each persistent volume.
      class: do-block-storage # Storage class for DigitalOcean block storage.
      deleteClaim: false # Prevents deletion of the PVC when the Kafka cluster is deleted.
  zookeeper:
    replicas: 3
    livenessProbe:
      initialDelaySeconds: 15
      timeoutSeconds: 5
    readinessProbe:
      initialDelaySeconds: 15
      timeoutSeconds: 5
    storage:
      type: persistent-claim # Persistent storage using PVCs.
      size: 100Gi # Size of each persistent volume.
      class: do-block-storage # Storage class for DigitalOcean block storage.
      deleteClaim: false # Prevents deletion of the PVC when the Zookeeper cluster is deleted.
  entityOperator:
    topicOperator: {} # Disable the topic operator by omitting configuration
    userOperator: {} # Enable the user operator by including an empty configuration
---
apiVersion: kafka.strimzi.io/v1beta2 # The version of the KafkaRebalance CRD API.
kind: KafkaRebalance # The type of Kubernetes resource, in this case, a KafkaRebalance.
metadata:
  name: cluster-name-rebalance # The name of this KafkaRebalance resource.
  namespace: kafka-connect # The namespace where the Strimzi operator is installed.
spec:
  goals:
    - CpuCapacityGoal
    - DiskCapacityGoal
    - NetworkInboundCapacityGoal
    - NetworkOutboundCapacityGoal
    - RackAwareGoal
    - ReplicaCapacityGoal
    - TopicReplicaDistributionGoal
---
```