# Setup cloud shell

```
npm i  @ibmgaragecloud/cloud-native-toolkit-cli

oc login --token=

oc new-project test-shell

export PATH=$PATH:/home/gsmolko/node_modules/@ibmgaragecloud/cloud-native-toolkit-cli

igc sync test-shell --dev

igc pipeline

```
