# Defining quotas for Openshift 
https://docs.openshift.com/container-platform/4.4/applications/quotas/quotas-setting-per-project.html

Sample yaml:


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
