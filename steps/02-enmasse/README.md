# EnMasse – Cloud scale messaging

Also see:

  * http://enmasse.io/

## Download

    curl -sL https://github.com/EnMasseProject/enmasse/releases/download/0.21.2/enmasse-0.21.2.tgz -o enmasse-0.21.2.tgz
    tar xzf enmasse-0.21.2.tgz

## Deploy

    oc new-project enmasse --display-name='EnMasse Instance'
    ./enmasse-0.21.2/deploy.sh -n enmasse

**Git for Windows:** You need to edit the `common.sh` file, locate the lines containing `\"/O=io.enmasse/CN=${CN}\"`
                     and replace them with `\"//O=io.enmasse\CN=${CN}\"`.

## Check readiness

Using the Web UI:

  * https://cluster00.amazing.iot-playground.org:8443
  * Navigate to the project "EnMasse Instance"
  * Check if the deployment `api-server` is ready

Using the command line:

    oc get deploy/api-server

## Fix endpoint certificates

    mkdir -p certs/{console,messaging,api-server}
    oc extract secret/external-certs-console --to=certs/console --confirm
    oc extract secret/external-certs-messaging --to=certs/messaging --confirm
    oc extract secret/api-server-cert --to=certs/api-server --confirm

    oc delete route/restapi route/console
    oc create route reencrypt console --service=console --dest-ca-cert=certs/console/ca.crt
    oc create route reencrypt restapi --service=api-server --dest-ca-cert=certs/api-server/tls.crt

## Deploy address resources

    curl -X POST -T addresses.json -H "content-type: application/json" https://$(oc -n enmasse get route restapi -o jsonpath='{.spec.host}')/apis/enmasse.io/v1alpha1/namespaces/enmasse/addressspaces/default/addresses

## Check resources

  * https://console-enmasse.cluster00.amazing.iot-playground.org
