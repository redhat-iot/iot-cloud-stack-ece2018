# Eclipse Che™ – Cloud IDE

## Deploy Che

Execute the following commands, be sure to replace `<initial-admin-password>`:

    cd che/deploy/openshift/templates
    
    oc new-project che --display-name='Eclipse Che'
    oc new-app -f multi/postgres-template.yaml -p CHE_VERSION=6.17.1
    oc new-app -f multi/keycloak-template.yaml -p KEYCLOAK_PASSWORD=<initial-admin-password> -p ROUTING_SUFFIX=[[cluster00]].amazing.iot-playground.org -p PROTOCOL=https
    oc apply -f pvc/che-server-pvc.yaml
    oc new-app -f che-server-template.yaml -p CHE_VERSION=6.17.1 -p ROUTING_SUFFIX=[[cluster00]].amazing.iot-playground.org -p CHE_MULTIUSER=true -p PROTOCOL=https -p WS_PROTOCOL=wss -p TLS=true
    oc set env dc/che CHE_MULTIUSER=true
    oc set volume dc/che --add -m /data --name=che-data-volume --claim-name=che-data-volume
    oc apply -f https
    
    cd ../../../..

**Git for Windows:** In the line `oc set volume dc/che --add -m /data --name=che-data-volume --claim-name=che-data-volume` replace `-m /data` with `-m //data`.

## First time login to Che

  * Go to: https://che-che.[[cluster00]].amazing.iot-playground.org
  * Register a new user
