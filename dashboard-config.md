# Configure developer dashboard

## Prerquisites:
Already installed all required tools: oc, node, igc, jq...

## Configure links in the development dashboard

Pipeline: 
`igc tool-config pipeline --url https://console-openshift-console.yourClusterName.domain/k8s/all-namespaces/tekton.dev~v1beta1~Pipeline`

LogDNA (copy link from LogDNA access link): 
`igc tool-config --name logdna --url https://app.eu-de.logging.cloud.ibm.com/f7cb48dce2/logs/view`


Sysdig (copy link from Sysdig access link): 
`igc tool-config --name sysdig --url https://eu-de.monitoring.cloud.ibm.com/#/explore/overview/l:3600/kubernetes.cluster.name%20=%20'cp4apps-tauron'/view.kubernetes.overview.cluster`


Image Registry (copy link from LogDNA access link): 
`igc tool-config --name ir --url https://cloud.ibm.com/kubernetes/registry/main/images?platformType=openshift`
