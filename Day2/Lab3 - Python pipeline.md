# Deploy Python application to the webapp instances we created previously
## On Day 1 of this course we saw insights on how a python web app deployment looks like
### Let's create ourselves the deployment pipeline

1. Open pipelines repository were lab files are located, you have 2 options:
    - from Github location: https://github.com/devschooldevops/07_08_pipelines
    - from Azure git repo in your project if the above repo was imported in Azure repo
2. Switch to branch **2024**
3. Download the file  `python-pipeline.yml`.
4. Go to Azure Devops Repos and check if you still have the imported repo `msdocs-python-flask-webapp-quickstart`
5. If not: 
    * import it by going to Repos - look to the top of your page, you should have your current repo selected
    * Click on arrow to expand the options and choose import repository

![import-repo](./images/import.png

6. After import go to Files then right tree dots menu
7. Upload files

![upload](./images/upload.png)

8. Upload `python-pipeline.yml` file downloaded previously
9. Now let's create the Pipeline by going to Pipelines - New pipeline
    * Choose Azure Repo `msdocs-python-flask-webapp-quickstart` 
    * Choose Existing Yaml pipeline...

    ![pipeline](./images/pipeline.png)

    * Select the path of the file `python-pipeline.yml` and click Continue
    * here we must add the 2 missing tasks we discussed in Day 1. Remember them? If not pls ask for help.

    :bulb: Use the task assistant to search for and load tasks in the pipeline, in this way we are sure no property is missed.
    
10. Run the pipeline targeting **test** webapp instance we created.
11. If results are ok, add another **stage** this time targeting **production** webapp instance.
12. Test the application by browsing the links in the pipeline logs.

How application in browser should look like:

![application](application.png)