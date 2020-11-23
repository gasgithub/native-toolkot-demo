# Setup additonal services

## LogDNA
Login to IBM Cloud 
In the Dashboar, select Observablility

Create new LogDNA instance
- select region
- select plan
- create instance

### Configure OpenShift cluster as source:
OpenShift

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

After you configure a log source, launch the LogDNA UI by selecting View LogDNA. It may take a few minutes before you start seeing logs.




