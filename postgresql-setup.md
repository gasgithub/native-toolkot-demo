# Instruction how to connect to postgres in IBM Cloud from OpenShift cluster

https://cloud.ibm.com/docs/databases-for-postgresql?topic=cloud-databases-tutorial-k8s-app

```
ibmcloud plugin install cloud-databases
ibmcloud login --sso
ibmcloud target -g Default
```
Bind service credentail:

Get service name: 
`ibmcloud resource service-instances`

Get cluster name:
`ibmcloud ks cluster ls`

Bind credential: 
```
ibmcloud ks cluster service bind --cluster <your_cluster_name> --namespace default --service <your_database_deployment>
```
