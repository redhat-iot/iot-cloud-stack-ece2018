# Eclipse Kura – Part 2

This step will setup up a build for Kura application, and deploy it to the running Kura instance.

## Register the device with Hono

First of all the Kura instance needs to be registered with Eclipse Hono:

    curl -X POST -H 'Content-Type: application/json' -d '{"device-id": "4711"}' https://hono-service-device-registry-http-hono.[[cluster00]].amazing.iot-playground.org/registration/DEFAULT_TENANT

## Connect to Kura

Next we need to connect the Kura gateway to Hono:

  * Go to the Kura Web UI: https://console-kura.[[cluster00]].amazing.iot-playground.org
  * Log in with: `admin` / `admin`
  * Navigate to: "Cloud Connections"
  * Select the list entry "Service PID" = "org.eclipse.kura.cloud.CloudService"
  * On the tab "CloudService":
    * `Encode gzip` = `false`
    * `Enable Default Subscriptions` = `false`
    * `Birth Cert Policy` = `Disable publishing`
    * `Payload Encoding` = `Simple JSON`
    * Press the "Apply" button -> Press "Yes"
  * On the tab "DataService":
    * `Connect Auto-on-startup` = `true`
    * `Store Housekeeper-interval` = `30`
    * `Enable Rate Limit` = `false`
    * Press the "Apply" button -> Press "Yes"
  * On the tab "MqttDataTransport"
    * `Broker-url` = `mqtt://hono-adapter-mqtt-vertx.hono.svc:1883/`
    * `Topic Context Account-Name` = `telemetry/DEFAULT_TENANT`
    * `Username` = `sensor1@DEFAULT_TENANT`
    * `Password` = `hono-secret`
    * `Client-id` = `4711`
    * Press the "Apply" button -> Press "Yes"
  * Press the "Connect/Disconnect" button

## Build and deploy

Edit the file `kura-app.yml` to put in your Git repository URL.

Execute the following commands to set up the pipeline build:

    oc project kura
    oc new-app jenkins-ephemeral
    oc create -f kura-app.yml

Wait until the Jenkins deployment is ready. Then navigate to "Build" -> "Pipelines" in
the OKD web UI. Open the pipeline "kura-app-generator-1" and start the pipeline by
pressing the "Start Pipeline" button.

After the build is complete, you should see a new Kura application named "Generator #1" in the Kura Web UI.

