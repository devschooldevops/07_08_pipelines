# Creating pipeline as code to build and deploy

## Prerequisites

- Azure subscription
- Available Azure Agent/Self hosted agent (**with git installed**)
- Available repository created in Azure DevOps
- Git token (Create one using this tutorial: https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token )

<br>

## Creation of a pipeline using the "as code" approach

### 1. In your newly created Azure DevOps repository navigate to the 3 dots -> **New** -> **File**

 ![](imgs/pac-create-pipeline-file.png)
<br>

### 2. Proceed and name the file '**pipeline.yaml**' and click **Create**. This will be our source code for the pipeline

 ![](imgs/pac-filename.png)
<br>

### 3. In the newly created 'pipeline.yaml' file, insert the following code-block which will create our pipeline orchestration

```yaml
# disable all pipeline triggers, so that our pipeline can run only manually
trigger: none

# Parameters keyword to signal that we will define one or more parameters
parameters:

# Defining a parameter for the git-token used in checking-out the app repository
- name: gitToken
  type: string
  default: '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'
  displayName: 'Git token used to clone the application repository'

# Stages keyword, signaling definition of one or multiple stages
stages:

# Defining our first stage for building the application
- stage: build_website_app
  displayName: 'Build Website application'
  pool:
    name: Default

# Jobs keyword, signaling definition of one or multiple jobs in the 'build_website_app' stage
  jobs: 

# Defining our first job
  - job: build_website_job
    displayName: 'Build website-app job'

# Adding the steps keyword to allow adding steps under the stage/job
    steps:
```
<br>

### 4. After defining the orchestration, we need to add the steps to build our website application

Insert the following code lines below the `steps` keyword, while paying attention to their respective comments

```yaml
  # Disable all of the downloads performed by the agent
    - download: none

  # Cloning the application repository from gitlab to our pipeline agent
    - bash: |
       git clone https://${{ parameters.gitToken }}@github.com/imhotepper/jsnoise-web-azdo.git
      displayName: 'Checkout app repo to agent'

  # Forcing the node tool version 14.x using a task
    - task: NodeTool@0
      displayName: 'Force Node Tool version 14.x'
      inputs:
        versionSpec: '14.x'
    
    # Install npm dependencies required by our application
    - task: Npm@1
      displayName: 'Install npm dependencies'
      inputs:
        command: 'install'
        workingDir: jsnoise-web-azdo

    
    # Build our website application
    - bash: |
        cd jsnoise-web-azdo
        npm run build
      displayName: 'Run build for website app'

    # Publish our built application, as an artifact in the pipeline
    # This artifact is needed so we can later deploy the application to Azure
    - task: PublishPipelineArtifact@1
      inputs:
        targetPath: 'jsnoise-web-azdo/dist'
        artifact: 'website'
        publishLocation: 'pipeline'
```
<br>

---
**NOTE**

We now have a complete build pipeline for our application!

---


### 5. We now need to set-up our deployment stage for the pipeline. In the same 'pipeline.yaml' we need to add another stage which will deploy our published artifact to an Azure storage account. Copy the below code after what is already existing and check the comments while doing so.

```yaml
# Defining our second stage for deploying the application
- stage: deploy_website_app
  displayName: 'Deploy Website application'
  dependsOn: build_website_app
  pool:
    name: Default

# Jobs keyword, signaling definition of one or multiple jobs in the 'deploy_website_app' stage
  jobs: 

# Defining our first job in the deployment stage
  - job: deploy_website_job
    displayName: 'Deploy website-app job'

# Adding the steps keyword to allow adding steps under the stage/job
    steps:

```
<br>

### 6. Add the following steps which will download our previously published artifact and will deploy it to our storage account.

```yaml
    # This task will download the website artifact on the agent
    # This is needed because each job is using a different agent and therefore for the deployment part
    # we don't have available what the build produced
    - task: DownloadPipelineArtifact@2
      inputs:
        buildType: 'current'
        artifactName: 'website'
        targetPath: 'website'
    
    # This script will run an az cli command to deploy our website to an Azure storage account
    - script: |
       az config set extension.use_dynamic_install=yes_without_prompt
       
       az storage blob directory upload -c '$web' --account-name ${{ parameters.accountName }} -s "website/*" -d . --recursive --account-key ${{ parameters.accountKey }}
      displayName: 'Deploy app to storage account'
```

### 7. We need to define the parameters used to authenticate in order to deploy the application to the storage account. In the 'parameters' section at the top of the pipeline file, add the following 2 parameters corresponding to our account name and account key.

```yaml
# Parameter to define input for account name
- name: accountName
  type: string

# Parameter to define input for the account key
- name: accountKey
  type: string
```

### 8. Now since our pipeline as code is ready, we need to create it in Azure DevOps and initiate a new run. Please follow the steps below.

- Navigate to the 'Pipelines' icon (Rocket) situated in the left side menu
- Click on 'New Pipeline'
- In the `Where is your code` screen, please select **Azure Repos Git**

![](imgs/pac-azure-repos-git.png)

- In the `Select a repository` screen, please pick the repository in which you created the pipeline.yaml file

![](imgs/pac-select-repo.png)

- In the `configure your pipeline` screen, please select **Existing Azure Pipelines YAML file**
- A window should pop up in the right side of the screen. Select the **branch** you created your pipeline in, and for the **path** select **pipeline.yaml**
- Click `continue`
- A new window should appear with your created pipeline. Just click `Run` at the top right of your screen

![](imgs/pac-select-pipeline-file.png)


---
**NOTE**

If after clicking run, you are presented with an error screen. Click on `Run new` at the top right corner. After clicking you will be presented with a window in the right side of the screen. Here we can see the parameters we added in the code.

- For the accountName and accoundKey ask one of the trainers for the values
- For the Git token field, if you haven't created one, you can use the defaulted one fron the `gitToken` parameter.

---

### 9. Make sure to cleanup by doing the following steps:

- Delete the `pipeline.yaml file` by clicking the 3 dots next to the file in the repository and then click `delete`
- Delete the actual pipeline by navigating to the `Pipelines` section in the left side menu, and next to the created pipeline click the 3 dots and then delete!
