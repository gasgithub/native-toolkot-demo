# Configure namespace to be able to pull images

## Config for internal OpenShift registry
```
oc policy add-role-to-user system:image-puller system:serviceaccount:inventory-management-staging:default --namespace=inventory-management
oc policy add-role-to-user system:image-puller system:serviceaccount:inventory-management-production:default --namespace=inventory-management
```

## Config for external IBM Cloud registry

Copy all-icr-io secret from default namespace to target namespace. 
Link pull secret:

```
oc secrets link default all-icr-io --for=pull
```
