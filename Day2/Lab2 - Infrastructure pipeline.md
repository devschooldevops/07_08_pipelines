# A pipeline can be used to create also the infrastructure environment for our application

## In this lab we will create 2 Azure App instances in Azure for our application

1. First create a new Azure Repository

![Create repo](repo.png)

2. Name it `infra-repo` and click Create 
3. Then go to Pipelines - New Pipeline - > Select your repository
4. Select starter pipeline
5. Add some variables:
    * `webappname: pythonapp`
    * `webappsuffix:` this values will be used to have unique webapp name, you can put your name or the suffix from devschool account. ex devschool_lotus will be **lotus**
    * `resourcegroup: ` the resource group name we created in previous lab
    * `plan: ` the name of the App service plan, can be same as resource group name + `-asp`
    * `environment`: 'test' - this should be the first value
5. Delete everyting under `steps:` block
6. Click on show assistant button to load the list of tasks
 ![assistant](assistant.png)
7. Search Az Cli and choose Azure Cli task
![azcli](azcli.png)
8. The Azure connection should be loaded automatically
9. For Script choose inline script
10. And for Inline script paste entire script below
8. Script:
`        webappsuffix=$(webappsuffix)

         az appservice plan create \
           --name $(plan)\
           --resource-group $(resourcegroup) \
           --sku B1 \
           --is-linux
        
        az webapp create \
        --name $(webappname)-$(environment)-$webappsuffix \
        --resource-group $(resourcegroup) \
        --plan $(plan)\
        --runtime "python|3.11"`
9. Check test webapp instance creation on Azure.
10. Let's create also the production instance:
    * Go to Repo Files and edit `azure-pipelines.yml`
    * update variable environment to have the value `production`
    * the pipeline should start again automatically and deploy the production instance
    * Check production instance presence