# Custom Bridge – From Hono to Kafka

The bridge is a small application which consumes the data from Eclipse Hono and "does something" with it.
Normally this would be a more sophisticated application, depending on your requirements.

In this case we simply forward the data from Eclipse Hono into a Kafka cluster.

Also see:

  * https://github.com/ctron/hono-example-bridge

## Deploy Bridge

    oc new-project hono-consumer --display-name 'Hono Consumer'
    oc new-app fabric8/s2i-java~https://github.com/<you>/hono-example-bridge#tutorial-ece2018 -e KAFKA_CLUSTER_NAME=hono-kafka-cluster -e KAFKA_PROJECT=kafka -e AMQP_HOST=messaging-hono-default.enmasse-infra.svc AMQP_USERNAME=consumer AMQP_PASSWORD=verysecret

## Fixing it up

    oc set probe dc/hono-example-bridge --readiness --liveness --get-url=http://:8080/health
    oc patch dc/hono-example-bridge --patch '{"spec":{"template":{"spec":{"containers":[{"name":"hono-example-bridge", "ports":[{"containerPort":8778, "name":"jolokia" }]}]}}}}'
