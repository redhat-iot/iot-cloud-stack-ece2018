# Custom Frontend – Kafka to the web

This is an example web frontend application. It acts as our custom "business systems".
It is written in TypeScript and will consume the payload data from the Kafka cluster.

Also see:

  * https://github.com/ctron/hono-example-demo-gauge

## Deploy Frontend

    oc new-project demo-gauge --display-name "Demo Gauge"
    oc new-app centos/nodejs-8-centos7~https://github.com/<you>/hono-example-demo-gauge#tutorial-ece2018 -e KAFKA_CLUSTER_NAME=hono-kafka-cluster -e KAFKA_PROJECT=kafka -e PAYLOAD_FORMAT=kura
    oc create route edge --service=hono-example-demo-gauge
