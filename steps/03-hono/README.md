# Eclipse Hono™ – IoT messaging

Also see:

  * https://eclipse.org/hono

## Deploy Hono

    oc new-project hono --display-name='Eclipse Hono'
    
    oc create configmap influxdb-config --from-file=influxdb.conf
    oc label configmap/influxdb-config app=hono-metrics
    
    oc create -f https://raw.githubusercontent.com/eclipse/hono/0.8.x/deploy/src/main/deploy/openshift_s2i/hono-address-space.yml
    oc process -f https://raw.githubusercontent.com/eclipse/hono/0.8.x/deploy/src/main/deploy/openshift_s2i/hono-template.yml -p GIT_BRANCH=0.8.x | oc create -f -
    oc create -f https://raw.githubusercontent.com/eclipse/hono/0.8.x/deploy/src/main/deploy/openshift_s2i/hono-tenant-template.yml
    oc process hono-tenant HONO_TENANT_NAME=DEFAULT_TENANT RESOURCE_NAME=defaulttenant CONSUMER_USER_NAME=consumer CONSUMER_USER_PASSWORD="$(echo -n verysecret | base64)"| oc create -f -

## Deploy metrics dashboard

    oc new-project grafana --display-name='Grafana Dashboard'
    
    oc create configmap grafana-provisioning-dashboards --from-file=grafana/provisioners
    oc create configmap grafana-dashboard-defs --from-file=grafana/dashboards
    oc label configmap grafana-provisioning-dashboards app=hono-metrics
    oc label configmap grafana-dashboard-defs app=hono-metrics
    
    oc process -f https://raw.githubusercontent.com/eclipse/hono/0.8.x/deploy/src/main/deploy/openshift_s2i/grafana-template.yml -p ADMIN_PASSWORD=admin -p GIT_BRANCH=0.8.x | oc create -f -

## Enable TLS

    oc -n grafana patch route/grafana -p '{"spec":{"tls":{"termination":"edge"}}}'
