# Create the development namespace

- Before getting started, the development namespace/project needs to be created and prepared for the DevOps pipelines.
- This is something that would typically happen once at the beginning of a project when a development team is formed and 
  assigned to the cluster.This step copies the common `secrets` and `configMaps` to your new namespace. This enables the pipelines to reference the values easily for you project

    ```
    oc sync {DEV_NAMESPACE} --dev
    ```

`oc sync` command is from toolkit not plain `oc`

### 3. Open the Developer Dashboard
- If you are logged into the OpenShift console, you can select the tools menu and select **Developer Dashboard**

- If you are on a laptop/desktop, open a browser and make sure you are logged into [Github](https://github.com)

- Open the dashboard by running the following command:
  ```
  oc dashboard
  ```
- From the Developer Dashboard, click on **<Globals name="templates" />** tab
- Pick one of the templates that is a good architectural fit for your application and the language and framework that you prefer to work with.

- Complete the [GitHub create repository from template](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/creating-a-repository-from-a-template)
process.

- Next, clone the Github repo to your local machine.

- You must rename the app to match your git repo or to a unique name for your solution. When applications move into a _test_ environment, they need to have unique names.

- In case of node app - Edit `package.json` and edit the `name:` field and change it from its template name to your chosen name.
- In case of a java gradle application(Spring Boot Microservice) -  edit the `settings.gradle` file. Edit the `rootProject.name` field and change it from its template name to your chosen name.


### Optionally - Run the application locally

### 7. Set the namespace context

Before running the remaining commands, it is important to set the
namespace/project context.

```shell script
oc project {DEV_NAMESPACE} 
```
### 8. Register the App in a DevOps Pipeline

Up to this point you have the code in a GitHub repository and have cloned it to your local development environment. You now need to register the repository with the continuous integration pipeline. The <Globals name="env" /> supports both [Tekton](/guides/continuous-integration-tekton) and [Jenkins](/guides/continuous-integration) for continuous
integration.

- Start the process to create a pipeline

    ```shell script
    oc pipeline
    ```

    <InlineNotification kind="info">

    The pipeline command give an option for both `Jenkins` and `Tekton`. For more information about working with the
    different build engines, please see [Continuous Integration with Jenkins Guide](/guides/continuous-integration) and
    [Continuous Integration with Tekton Guide](/guides/continuous-integration-tekton)

    </InlineNotification>

- For the deployment of your first app with OpenShift select **Tekton** as the chosen CI engine.

- The first time a pipeline is registered in the namespace, the CLI will ask for a username and
**Personal Access Token** for the Git repository that will be stored in a secret named `git-credentials`. It will
also ask for the branch that should be used for the pipeline.

  **Username**: Enter your GitHub user id

  **Personal Access Token**: Paste your GitHub personal access token

  **Branch**: Press enter to use the default git branch, master, or type in another branch you want to register

- When registering a `Tekton` pipeline, you will be prompted to select which pipeline you want to use for your application. If you selected Node based Code Pattern, select the Node pipeline. If you selected Java, select the Gradle pipeline.
- For the first app, select the `igc-nodejs-v1-x-0` version of the pipeline. This will use the Node based CI pipeline with Tekton.
    ```
    ? Select the Pipeline to use in the PipelineRun: (Use arrow keys)❯
     igc-appmod-liberty-v1-2-0
     igc-java-gradle-v1-2-0
     igc-java-maven-v1-2-0
     igc-nodejs-v1-2-0
     Skip PipelineRun creation
    ```
- It also gives you a option of vulnerability scanning the images.The scan is performed by the Vulnerability Advisor of IBM Image Registry. This scan is performed in "scan" stage of pipeline after "img-release" stage.
  ```
  ? Would you like to enable the pipeline to scan the image for vulnerabilities?(Y/n)
  ```
- To skip the scan, you have type "n" (No).Otherwise, type "y" (Yes) for performing Vulnerability Scanning on the image.

- After the pipeline has been created,the command will set up a webhook from the Git host to the pipeline event listener

    **Note:** if the webhook registration step fails, it is likely because the Git credentials are incorrect or do not have enough permission in the repository. 

- The pipeline will be registered in your development cluster.

