# Steps to create autoscaler 
https://docs.openshift.com/container-platform/4.4/nodes/pods/nodes-pods-autoscaling.html

Add limits to container resources:

```
    resources:
      requests:
        cpu: 50m 
        memory: 100Mi 
      limits:
        cpu: 100m 
        memory: 200Mi 
```        

create HorizontalPodAutoscaler

```
kind: HorizontalPodAutoscaler
apiVersion: autoscaling/v2beta1
metadata:
  name: demo-node-typescript
  namespace: demo-node-typescript
  labels:
    app: demo-node-typescript
spec:
  scaleTargetRef:
    kind: Deployment
    name: demo-node-typescript
    apiVersion: apps/v1
  minReplicas: 1
  maxReplicas: 3
  metrics:
    - type: Resource
      resource:
        name: cpu
        targetAverageUtilization: 30
```    


Template for the helm chart:

```
kind: HorizontalPodAutoscaler
apiVersion: autoscaling/v2beta1
metadata:
  name: demo-node-typescript
  namespace: demo-node-typescript
  labels:
    app: demo-node-typescript
spec:
  scaleTargetRef:
    kind: Deployment
    name: demo-node-typescript
    apiVersion: apps/v1
  minReplicas: 1
  maxReplicas: 3
  metrics:
    - type: Resource
      resource:
        name: cpu
        targetAverageUtilization: 30

```
