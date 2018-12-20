##  Running Debezium on Kubernetes/OpenShift

**Note**: This project is archived. The [recommended way](https://debezium.io/docs/openshift/) for running Debezium as well as Apache Kafka, Kafka Connect on ZooKeeper on Kubernetes and distributions such as OpenShift is to use the custom resource definitions (CRDs) and operators provided by the [Strimzi](http://strimzi.io/) project.

This project builds the kubernetes manifest files for running Zookeeper (standalone at the moment), Apache Kafka, Kafka Connect with the Debezium MySQL connector and a MySQL 5.6 database on Kubernetes. The project uses the awesome [fabric8-maven-plugin](http://fabric8.io/guide/mavenPlugin.html) for automatically generating the manifest in both `json` and `yaml` formats. 

To build, go to the root of this project and run:

> mvn clean install

Then you can look in the `target/classes` folder of each subproject and see the `kubernees.json` and `kubernetes.yml` files. Each file specifies a Kubernetes [ReplicationController](http://kubernetes.io/docs/user-guide/replication-controller/) (now named ReplicaSet in Kubernetes 1.2+) and a Kubernetes [Service](http://kubernetes.io/docs/user-guide/services/).
 
If you're logged in to a Kubernees cluster, you can deploy the json/yml with maven:

> mvn fabric8:apply

This will read your `~/.kube/config` file and deploy it into the namespace which is in your current context. Please see the  [fabric8-maven-plugin documentation for more details and fine grained control.](http://fabric8.io/guide/mavenPlugin.html).

If you don't want to use Maven to deploy, you can use the `kubectl` tool directly. For example:

> kubectl create -f zk-standalone/target/classes/kubernetes.yml

