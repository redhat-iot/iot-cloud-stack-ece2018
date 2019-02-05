# EnMasse – Cloud scale messaging

Also see:

  * http://enmasse.io/

## Download

    curl -LO https://github.com/EnMasseProject/enmasse/releases/download/0.26.2/enmasse-0.26.2.tgz
    tar xzf enmasse-0.26.2.tgz

## Deploy

    oc login -u admin
    oc new-project enmasse-infra --display-name='EnMasse'
    oc apply -f enmasse-0.26.2/install/bundles/enmasse-with-standard-authservice

## Check readiness

Using the Web UI:

  * https://[[cluster00]].amazing.iot-playground.org:8443
  * Navigate to the project "EnMasse Instance"
  * Check if the deployment `api-server` is ready

Using the command line:

    oc get deploy/api-server deploy/keycloak

Verify that the "AVAILABLE" column shows "1":

    NAME         DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
    api-server   1         1         1            1           1m
    keycloak     1         1         1            1           1m

## Switch back to normal user

    oc login -u developer
