# Steps of the tutorial

These are the steps of the tutorial:

* [Step 0 – Getting Started](00-getting-started)
* [Step 1 – Creating an IoT gateway container](01-kura-part-1)
* [Step 2 – Deploying EnMasse](02-enmasse)
* [Step 3 – Deploying Eclipse Hono](03-hono)
* [Step 4 – Deploy a Kafka cluster with Strimzi](04-strimzi)
* [Step 5 – Bridging Hono and Kafka](05-bridge)
* [Step 6 – Web Frontend](06-frontend)
* [Step 7 – Kura Application](07-kura-part-2)
* [Step 8 – Deploying Eclipse Che](08-che-part-1)
* [Step 9 – Importing projects](09-che-part-2)
* [Step 10 – Making changes](10-che-part-3)

The following steps assume, that the DNS name of your OKD cluster
is `<<clusterXX>>.amazing.iot-playground.org`, if your DNS name is different
(which should be the case) then you need to replace this in all commands and links.
You'll probably just change `<clusterXX>` with your exact cluster, like `<clusterXX>` for example.

The same is true for some (not all) Git URLs. Some URL are in the form `git@github.com:<you>/foo-bar.git`.
In this case you need to have a clone of that repository and replace `<you>` with
your account name. Or use a custom Git URI altogether.

This tutorial assumes that your shell is in the actual sub-directory of the step
when executing commands.
