# Strimzi – Kafka Cluster

Also see: 

  * http://strimzi.io/

---

**Sed for OSX**

`sed` for OSX works differently than on Linux, the easiest way around it to use the gnu-sed tool:

    brew install gnu-sed

You then need to replace `sed` later on with `gsed`.

---

## Create Kafka cluster

    sed -i 's/namespace: .*/namespace: kafka/' strimzi/install/cluster-operator/*RoleBinding*.yaml

    oc login -u admin

    oc new-project kafka  --display-name='Kafka Cluster'
    oc apply -f strimzi/install/cluster-operator
    oc apply -f kafka

    oc login -u developer
