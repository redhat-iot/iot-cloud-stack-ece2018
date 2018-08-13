# Eclipse Hono™ – IoT messaging

Also see:

  * https://eclipse.org/hono

## Deploy Hono

    oc new-project hono --display-name='Eclipse Hono'
    
    oc create configmap influxdb-config --from-file=influxdb.conf
    oc label configmap/influxdb-config app=hono-metrics
    
    oc process -f https://raw.githubusercontent.com/eclipse/hono/0.7.x/deploy/src/main/deploy/openshift_s2i/hono-template.yml -p ENMASSE_NAMESPACE=enmasse -p GIT_BRANCH=0.7.x | oc create -f -

## Deploy metrics dashboard

    oc new-project grafana --display-name='Grafana Dashboard'
    
    oc create configmap grafana-provisioning-dashboards --from-file=grafana/provisioners
    oc create configmap grafana-dashboard-defs --from-file=grafana/dashboards
    oc label configmap grafana-provisioning-dashboards app=hono-metrics
    oc label configmap grafana-dashboard-defs app=hono-metrics
    
    oc process -f https://raw.githubusercontent.com/eclipse/hono/0.7.x/deploy/src/main/deploy/openshift_s2i/grafana-template.yml -p ADMIN_PASSWORD=admin -p GIT_BRANCH=0.7.x | oc create -f -

## Enable TLS

    oc -n grafana patch route/grafana -p '{"spec":{"tls":{"termination":"edge"}}}'
    oc -n hono patch route/hono-service-device-registry-http -p '{"spec":{"tls":{"termination":"edge"}}}'
