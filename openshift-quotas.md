# Defining quotas for Openshift 
https://docs.openshift.com/container-platform/4.4/applications/quotas/quotas-setting-per-project.html

Sample yaml:
```
apiVersion: v1
kind: ResourceQuota
metadata:
  name: test-project-quota
spec:
  hard:
    configmaps: "10" 
    secrets: "10" 
    services: "10" 
    pods: "4" 
    requests.cpu: "1" 
    requests.memory: 1Gi 
    limits.cpu: "2" 
    limits.memory: 2Gi 
```    

## Table 1. Compute resources managed by quota

|Resource Name|Description|
|--- |--- |
|cpu|The sum of CPU requests across all pods in a non-terminal state cannot exceed this value. cpu and requests.cpu are the same value and can be used interchangeably.|
|memory|The sum of memory requests across all pods in a non-terminal state cannot exceed this value. memory and requests.memory are the same value and can be used interchangeably.|
|ephemeral-storage|The sum of local ephemeral storage requests across all pods in a non-terminal state cannot exceed this value. ephemeral-storage and requests.ephemeral-storage are the same value and can be used interchangeably. This resource is available only if you enabled the ephemeral storage technology preview. This feature is disabled by default.|
|requests.cpu|The sum of CPU requests across all pods in a non-terminal state cannot exceed this value. cpu and requests.cpu are the same value and can be used interchangeably.|
|requests.memory|The sum of memory requests across all pods in a non-terminal state cannot exceed this value. memory and requests.memory are the same value and can be used interchangeably.|
|requests.ephemeral-storage|The sum of ephemeral storage requests across all pods in a non-terminal state cannot exceed this value. ephemeral-storage and requests.ephemeral-storage are the same value and can be used interchangeably. This resource is available only if you enabled the ephemeral storage technology preview. This feature is disabled by default.|
|limits.cpu|The sum of CPU limits across all pods in a non-terminal state cannot exceed this value.|
|limits.memory|The sum of memory limits across all pods in a non-terminal state cannot exceed this value.|
|limits.ephemeral-storage|The sum of ephemeral storage limits across all pods in a non-terminal state cannot exceed this value. This resource is available only if you enabled theephemeral storage technology preview. This feature is disabled by default.|

## Table 2. Storage resources managed by quota 

|Resource Name|Description|
|--- |--- |
|requests.storage|The sum of storage requests across all persistent volume claims in any state cannot exceed this value.|
|persistentvolumeclaims|The total number of persistent volume claims that can exist in the project.|
|*storage-class-name*.storageclass.storage.k8s.io/requests.storage|The sum of storage requests across all persistent volume claims in any state that have a matching storage class, cannot exceed this value.|
|*storage-class-name*.storageclass.storage.k8s.io/persistentvolumeclaims|The total number of persistent volume claims with a matching storage class that can exist in the project.|
  
## Table 3. Object counts managed by quota

|Resource Name|Description|
|--- |--- |
|pods|The total number of pods in a non-terminal state that can exist in the project.|
|replicationcontrollers|The total number of ReplicationControllers that can exist in the project.|
|resourcequotas|The total number of resource quotas that can exist in the project.|
|services|The total number of services that can exist in the project.|
|services.loadbalancers|The total number of services of type LoadBalancer that can exist in the project.|
|services.nodeports|The total number of services of type NodePort that can exist in the project.|
|secrets|The total number of secrets that can exist in the project.|
|configmaps|The total number of ConfigMap objects that can exist in the project.|
|persistentvolumeclaims|The total number of persistent volume claims that can exist in the project.|
|openshift.io/imagestreams|The total number of imagestreams that can exist in the project.|  
  
# Quotas for multiple projects

```
apiVersion: v1
kind: ClusterResourceQuota
metadata:
  name: for-user
spec:
  quota: 
    hard:
      pods: "10"
      secrets: "20"
  selector:
    annotations: 
      openshift.io/requester: <user_name>
    labels: null 
status:
  namespaces: 
  - namespace: ns-one
    status:
      hard:
        pods: "10"
        secrets: "20"
      used:
        pods: "1"
        secrets: "9"
  total: 
    hard:
      pods: "10"
      secrets: "20"
    used:
      pods: "1"
      secrets: "9"
```  
