## common config 
1. replica
	The type of replication depends on the resource.
	
	- `KafkaTopic` uses a replication factor to configure the number of replicas of each partition within a Kafka cluster.
	    
	- Kafka components use replicas to configure the number of pods in a deployment to provide better availability and scalability.
2. bootstrapServers
	The bootstrap server lists can refer to Kafka clusters that are not deployed in the same Kubernetes cluster. They can also refer to a Kafka cluster not deployed by Strimzi.
3. SSL 
	The `ssl.enabled.protocols` property specifies the available TLS versions that can be used for secure communication between the cluster and its clients. The `ssl.protocol` property sets the default TLS version for all connections, and it must be chosen from the enabled protocols. Use the `ssl.endpoint.identification.algorithm` property to enable or disable hostname verification (configurable only in components based on Kafka clients - Kafka Connect, MirrorMaker 1/2, and Kafka Bridge).
	- AES (Advanced Encryption Standard) encryption (256-bit key)
	- GCM (Galois/Counter Mode) authenticated encryption
	- SHA384 (Secure Hash Algorithm) data integrity protection
4. trustedCertificates
	Having set `tls` to configure TLS encryption, use the `trustedCertificates` property to provide a list of secrets with key names under which the certificates are stored in X.509 format.
	You can use the secrets created by the Cluster Operator for the Kafka cluster, or you can create your own TLS certificate file, then create a `Secret` from the file:
	```
	kubectl create secret generic _MY-SECRET_ \ --from-file=_MY-TLS-CERTIFICATE-FILE.crt
	```
	example:
	```
	tls:
	   trustedCertificates:
	     - secretName: my-cluster-cluster-cert
	       certificate: ca.crt
	     - secretName: my-cluster-cluster-cert
	       certificate: ca2.crt
	
	```
5.  jvmOptions
	`-Xms`
	Minimum initial allocation heap size when the JVM starts
	`-Xmx`
	Maximum heap size
	`-XX`
	Advanced runtime options for the JVM.  Options are used to configure the KAFKA_JVM_PERFORMANCE_OPTS option of Apache Kafka.
	`javaSystemProperties`
	Additional system properties.
	
	The `jvmOptions` property also allows you to enable and disable garbage collector (GC) logging. GC logging is disabled by default. To enable it, set the `gcLoggingEnabled` property as follows:
	```
	jvmOptions: 
	     gcLoggingEnabled: true 
    ```
6. Listeners
use the `listeners` property to configure listeners to provide access to Kafka brokers.
```
apiVersion: kafka.strimzi.io/v1beta2
kind: Kafka
spec:
  kafka:
    listeners:
      - name: plain
         port: 9092
         type: internal
         tls: false
zookeeper:
```
Example Kafka broker configuration
```
apiVersion: kafka.strimzi.io/v1beta2
kind: Kafka
metadata:
  name: my-cluster
spec:
  kafka:
    config:
	  num.partitions: 1
	  num.recovery.threads.per.data.dir: 1
	  default.replication.factor: 3
	  offsets.topic.replication.factor: 3
	  transaction.state.log.replication.factor: 3
	  transaction.state.log.min.isr: 1
	  log.retention.hours: 168
	  log.segment.bytes: 1073741824
	  log.retention.check.interval.ms: 300000
	  num.network.threads: 3
	  num.io.threads: 8
	  socket.send.buffer.bytes: 102400
	  socket.receive.buffer.bytes: 102400
	  socket.request.max.bytes: 104857600
	  group.initial.rebalance.delay.ms: 0
	  zookeeper.connection.timeout.ms: 6000
```
7. Logging
	Kafka uses the Apache `log4j` logger implementation.
	Inline logging:
	```
	apiVersion: kafka.strimzi.io/v1beta2
	kind: Kafka
	spec:
	  kafka:
	    logging:
	      type: inline
	      loggers:
			kafka.root.logger.level: INFO
			log4j.logger.kafka.coordinator.transaction: TRACE
			log4j.logger.kafka.log.LogCleanerManager: DEBUG
			log4j.logger.kafka.request.logger: DEBUG
			log4j.logger.io.strimzi.kafka.oauth: DEBUG
			log4j.logger.org.openpolicyagents.kafka.OpaAuthorizer: DEBUG
	```
	External logging:
	```
	apiVersion: kafka.strimzi.io/v1beta2
	kind: Kafka
	spec:
	  kafka:
	    logging:
	      type: external
	      valueFrom:
	        configMapKeyRef:
	          name: customConfigMap
	          key: kafka-log4j.properties
	```

8. GenericKafkaListener
	 Used in: [`KafkaClusterSpec`](https://strimzi.io/docs/operators/latest/configuring.html#type-KafkaClusterSpec-reference)
	 
	Configures listeners to connect to Kafka brokers within and outside Kubernetes.
	You configure the listeners in the `Kafka` resource.
	Example `Kafka` resource showing listener configuration:
	```
	apiVersion: kafka.strimzi.io/v1beta2
	kind: Kafka
	metadata:
	  name: my-cluster
	spec:
	  kafka:
		listeners:
		  - name: plain
		    port: 9092
			type: internal
			tls: false
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
		  - name: external2
			port: 9095
			type: ingress
			tls: true
			authentication:
			  type: tls
			configuration:	
			  bootstrap:	
				host: bootstrap.myingress.com	
			  brokers:	
			  - broker: 0	
			    host: broker-0.myingress.com	
			  - broker: 1	
			    host: broker-1.myingress.com	
			  - broker: 2	
			    host: broker-2.myingress.com
		
	```