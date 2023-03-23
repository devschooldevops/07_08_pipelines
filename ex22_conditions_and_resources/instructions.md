Let's dive deeper in resources and conditions:

* Create a repo called "Templates"
* Create a folder called "vars" inside the new repo and a file called vars.yml inside it (copy the contents from vars.yml)
* Create a folder called "thetemplates" inside the new repo and copy the rest of the templates from the templates folder inside it
* Create a repo where we will have the main pipeline (pipeline.yml)
* Run the main pipeline after you modify the pipeline.yml file with your organization
* Create 2 more stages
* Use dependsOn and condition directives on them https://learn.microsoft.com/en-us/azure/devops/pipelines/process/stages?view=azure-devops&tabs=yaml 
* Let's create some conditions together!