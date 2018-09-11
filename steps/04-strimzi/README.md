# Strimzi – Kafka Cluster

Also see: 

  * http://strimzi.io/

## Deploy Strimzi

    sed -i 's/namespace: .*/namespace: strimzi/' strimzi/examples/install/cluster-operator/*ClusterRoleBinding*.yaml

---
**Sed for OSX:**

sed for OSX works differently than on Linux, the easiest way around it to use gnu-sed tool

    brew install gnu-sed
    gsed -i 's/namespace: .*/namespace: strimzi/' strimzi/examples/install/cluster-operator/*ClusterRoleBinding*.yaml

After this step, you can continue with usual steps
---

    oc login -u admin

    oc new-project strimzi --display-name='Strimzi'
    oc create -f strimzi/examples/install/cluster-operator
    oc create -f strimzi-admin.yml
    oc set env deployment/strimzi-cluster-operator STRIMZI_NAMESPACE=strimzi,kafka

    oc adm policy add-cluster-role-to-user StrimziAdmin developer

    oc login -u developer

## Create Kafka cluster

    oc new-project kafka  --display-name='Kafka Cluster'
    oc apply -f kafka
