controllers control loops. our loop has 3 stages :
1. observe
	this section handle by custom resource in this article it's mean do it by rabbitmq cluster . 
2. analyze
	with the previews state now analyze what do we need. we need these object:
		1. statefulset : pods spec in rabbitmq cluster
		2. service: route traffic from client to rabbitmq
		3. configmap: API plugin for rabbitmq
		4. configmap: for configuration rabbitmq
		6. secret: for default username and pass
		7. secret: for cookies for rabbitmq knows each other
3.. act
How Rabbitmq Operator work:

User -- involve some yaml files --- kubectl --> k8s API --> cluster operator --> RMQ-cluster1, RMQ-cluster2

when you create manifest and define kind is RabbitmqCluster you create and config your rabbit clusters.

install operator :
1. go to the github and install new version
`https://github.com/rabbitmq/cluster-operator/releases/latest/download/cluster-operator.yml`
