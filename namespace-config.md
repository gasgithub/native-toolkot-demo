# Configure namespace to be able to pull images

## Config for internal OpenShift registry
```
oc policy add-role-to-user system:image-puller system:serviceaccount:inventory-management-staging:default --namespace=inventory-management
oc policy add-role-to-user system:image-puller system:serviceaccount:inventory-management-production:default --namespace=inventory-management
```

## Config for external IBM Cloud registry

