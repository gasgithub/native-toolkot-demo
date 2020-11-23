# native-toolkot-demo

## install toolkit
https://cloudnativetoolkit.dev/getting-started-day-0/install-toolkit/quick-install

Run the installation using the OpenShift CLI 
MAC/Linux 
```
curl -sfL get.cloudnativetoolkit.dev | sh -
```
Winddows 
```
oc create -f https://raw.githubusercontent.com/ibm-garage-cloud/ibm-garage-iteration-zero/master/install/install-ibm-toolkit.yaml
sleep 5
oc wait pod -l job-name=ibm-toolkit --for=condition=Ready -n default
oc logs job/ibm-toolkit -f -n default
```

## install cli tools
https://cloudnativetoolkit.dev/getting-started/prereqs

Github Personal Access Token
Navigate to Developer Settings and generate a new token; name it something like “CI pipeline”
Select public_repo scope to enable git clone
Select write:repo_hook scope so the pipeline can create a web hook 


The following is a list of desktop tools required to help with installation and development.

- [Git Client](https://git-scm.com/): Needs to be installed in your development operating system, it comes as standard for Mac OS

- [IBM Cloud CLI](https://cloud.ibm.com/docs/cli?topic=cloud-cli-getting-started): Required for management of IBM Cloud Account and management of your managed IBM Kubernetes and Red Hat OpenShift clusters
    - Don't install just the [IBM Cloud CLI](https://cloud.ibm.com/docs/cli?topic=cloud-cli-install-ibmcloud-cli), install the [IBM Cloud CLI and Developer Tools](https://cloud.ibm.com/docs/cli?topic=cloud-cli-getting-started#step1-install-idt)
    ```shell script
    curl -sL https://ibm.biz/idt-installer | bash
    ```
    - Note: If you log in to the web UI using SSO, you'll need to 
    [create an API key](https://cloud.ibm.com/docs/iam?topic=iam-federated_id) for logging into the CLI. (You can also 
    use this API key for [installing with the <Globals name="shortName" />](/getting-started-day-0).)

- [OpenShift OC CLI](https://mirror.openshift.com/pub/openshift-v4/clients/ocp/latest/): Required for Red Hat OpenShift management and development
    - Download the appropriate **client** tar ball
    - Open a terminal and change to the directory where the tar ball was downloaded
    - Create a directory for the tar ball contents
    ```shell script
    mkdir ./openshift-client
    ```
    - Change to the new `openshift-client` directory and unpack the tar ball
    ```shell script
    cd openshift-client
    tar xzf ../openshift-client-{platform}-{version}.tar.gz
    ```
    - Copy the `oc` and `kubectl` commands from the unpacked folder into your Terminal `PATH` (e.g. /usr/local/bin)
    ```shell script
    cp kubectl /usr/local/bin
    cp oc /usr/local/bin
    ```
    <br/>
    
    
- [Docker Desktop](https://www.docker.com/products/docker-desktop): Required for running common tools and [Developer Tools Image](/tools/tools-image)
    - Installed and running on your local machine

- [Node](https://nodejs.org/en/): Required for running the [IBM Garage for Cloud CLI](/getting-started/cli)
    - Installed on your local machine
    - Recommended `v12.x LTS`

- [IBM Garage for Cloud CLI](https://cloudnativetoolkit.dev/getting-started/cli): Used to help make working with the development tools as easy as possible
    ```shell script
    npm i -g @ibmgaragecloud/cloud-native-toolkit-cli
    ```
  
    *Note:* If you are adventurous, you can install the beta version of the cli that contains upcoming features with the 
    following command (switch back at any time with the above command):
    ```shell script
    npm i -g @ibmgaragecloud/cloud-native-toolkit-cli@beta
    ```

