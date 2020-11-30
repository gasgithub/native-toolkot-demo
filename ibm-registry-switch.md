# Steps to use IBM registry instead of openshift one

Edit registry-config secret to add following keys:

```
data:
  REGISTRY_NAMESPACE: reg namespace
  REGISTRY_PASSWORD: ibm api key
  REGISTRY_URL: reg url
  REGISTRY_USER: iamapikey
```
