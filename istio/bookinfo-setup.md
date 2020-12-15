# Bookinfo with Istio/OpenShift Mesh

## Install Openshift service mesh
Install mesh if not currently installed - https://docs.openshift.com/container-platform/4.4/service_mesh/v1x/installing-ossm.html

## Create `istio-system` project
Create project if not exists:

```
oc new-project istio-system
```

wait till all operators are successfully installed:

```
oc -n istio-system get csv
NAME                                            DISPLAY                          VERSION                  REPLACES   PHASE
appsody-operator.v0.5.1                         Appsody Operator                 0.5.1                               Succeeded
elasticsearch-operator.4.3.40-202010141211.p0   Elasticsearch Operator           4.3.40-202010141211.p0              Succeeded
jaeger-operator.v1.17.7                         Red Hat OpenShift Jaeger         1.17.7                              Succeeded
kiali-operator.v1.24.2                          Kiali Operator                   1.24.2                              Succeeded
open-liberty-operator.v0.5.1                    Open Liberty Operator            0.5.1                               Succeeded
openshift-pipelines-operator.v0.11.2            OpenShift Pipelines Operator     0.11.2                              Succeeded
serverless-operator.v1.7.2                      OpenShift Serverless Operator    1.7.2                               Succeeded
servicemeshoperator.v2.0.0.2                    Red Hat OpenShift Service Mesh   2.0.0-2                             Succeeded
```

## Create `bookinfo` project

```
oc new-project bookinfo
```

## Configure Mesh control plane
You can do it via web console or command line -https://docs.openshift.com/container-platform/4.4/service_mesh/v1x/installing-ossm.html#ossm-control-plane-deploy-1x_installing-ossm-v1x

##  Create Istio Service Mesh Member Roll
Create default roll, add `bookinfo` project to members

# Preparing application

## Enabling cart injection
When deploying an application into the Red Hat OpenShift Service Mesh you must opt in to injection by specifying the sidecar.istio.io/inject annotation with a value of "true".

```
  template:
    metadata:
      annotations:
        sidecar.istio.io/inject: "true"
```

## Deploy application 
Deploy application:
```
oc apply -n bookinfo -f https://raw.githubusercontent.com/Maistra/istio/maistra-1.1/samples/bookinfo/platform/kube/bookinfo.yaml
```

Create the ingress gateway by applying the bookinfo-gateway.yaml file:
```
oc apply -n bookinfo -f https://raw.githubusercontent.com/Maistra/istio/maistra-1.1/samples/bookinfo/networking/bookinfo-gateway.yaml
```

## Check ingress gateway route:

Should be something like:
```	
oc -n istio-system get route istio-ingressgateway -o jsonpath='{.spec.host}'

http://istio-ingressgateway-istio-system.clusterName
```

## Create default routes
```
oc apply -n bookinfo -f https://raw.githubusercontent.com/Maistra/istio/maistra-1.1/samples/bookinfo/networking/destination-rule-all.yaml
```

