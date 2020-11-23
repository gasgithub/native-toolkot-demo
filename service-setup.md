# Setup additonal services

## LogDNA
Login to IBM Cloud 
In the Dashboar, select Observablility > Logging

Create new LogDNA instance
- select region
- select plan
- create instance

### Configure OpenShift cluster as source:
Click `Edit Sources` link and select `OpenShift` tab:

Note that the user or service ID that is used to deploy the agent requires IAM permissions.

1. Create a project. A project is a namespace in a cluster.

`oc adm new-project --node-selector='' ibm-observe`

2. Create the service account logdna-agent in the cluster namespace ibm-observe.

`oc create serviceaccount logdna-agent -n ibm-observe`

3. Grant the service account access to the Privileged SCC:

`oc adm policy add-scc-to-user privileged system:serviceaccount:ibm-observe:logdna-agent`

4. Add your secret: 

`oc create secret generic logdna-agent-key --from-literal=logdna-agent-key=yourLogKey -n ibm-observe`


5. Install the OpenShift DaemonSet:

`oc create -f https://assets.eu-de.logging.cloud.ibm.com/clients/logdna-agent-ds-os.yaml -n ibm-observe`

After you configure a log source, check if all the pods are running correctly in the ibm-observe namespace, then launch the LogDNA UI by selecting 'View LogDNA'. It may take a few minutes before you start seeing logs.

Link to LogDNA - https://app.eu-de.logging.cloud.ibm.com/f7cb48dce2/logs/view

## Configure Sysdig

Login to IBM Cloud 
In the Dashboar, select Observablility > Monitoring

Create new Sysdig instance
- select region
- select plan
- create instance

### Configure OpenShift cluster as source:
Click `Edit Sources` link and select `OpenShift` tab:

Set up your Red Hat OpenShift on IBM Cloud cluster with a Sysdig DaemonSet to forward cluster metrics such as worker node CPU and memory usage, HTTP traffic in and out of your containers, and data about other infrastructure components. For more information, see the docs.

1. From the OpenShift > Clusters page, select your cluster, click the Access tab, and follow the instructions to log in to your cluster with the CLI.

2. Install the Sysdig agent in your cluster. (make sure you are logged in to correct account using `ibmcloud login` before executing folllowing):

Public Endpoint

curl -sL https://ibm.biz/install-sysdig-k8s-agent | bash -s -- -a yourSysdigKey -c ingest.eu-de.monitoring.cloud.ibm.com -ac 'sysdig_capture_enabled: false' --openshift

```
* Detecting operating system
* Downloading Sysdig cluster role yaml
* Downloading Sysdig config map yaml
* Downloading Sysdig daemonset v2 yaml
* Downloading Sysdig agent-slim daemonset v2 yaml
* Creating project: ibm-observe
oc adm new-project failed!
error: project ibm-observe already exists. Continuing...
* Creating sysdig-agent serviceaccount in project: ibm-observe
oc create serviceaccount failed!
Error from server (AlreadyExists): serviceaccounts "sysdig-agent" already exists. Continuing...
* Creating sysdig-agent access policies
* Creating sysdig-agent secret using the ACCESS_KEY provided
kubectl create secret failed!
Error from server (AlreadyExists): secrets "sysdig-agent" already exists. Re-creating secret...
secret "sysdig-agent" deleted
secret/sysdig-agent created
* Retreiving the IKS Cluster ID and Cluster Name
* Setting cluster name as cp4apps-tauron
* Setting ibm.containers-kubernetes.cluster.id burphuff0acovdqdl8ng
* Updating agent configmap and applying to cluster
* Setting tags
* Setting collector endpoint
* Adding additional configuration to dragent.yaml
* Enabling Prometheus
secret "all-icr-io" deleted
Processing all-icr-io as all-icr-io
secret/all-icr-io created
configmap/sysdig-agent configured
* Deploying the sysdig agent
daemonset.apps/sysdig-agent configured
```

Check Sysdig for updates once you successfully add or remove agents. It may take a couple minutes.

Link to Sysdig: 
https://eu-de.monitoring.cloud.ibm.com/#/explore/overview/l:3600/kubernetes.cluster.name%20=%20'cp4apps-tauron'/view.kubernetes.overview.cluster

## Configure Image Regsirty 

Login to IBM Cloud 
In the Dashboar, select OpenShift > Registry

Create new namespace:
- select region
- select `Namespaces` tab
- click `Create` and provide name e.g. `poc-registry` 

Link to images: https://cloud.ibm.com/kubernetes/registry/main/images?platformType=openshift
