# Lab1 - Starter - pipeline

1. Sign in to your Azure DevOps organization (https://dev.azure.com/[organization]) and go to your project.
2. Import repository https://github.com/devschooldevops/07_08_pipelines.git
    - Go to Repos - Files
    - Import a repository -> Import
    - Clone URL: https://github.com/devschooldevops/07_08_pipelines.git
    - Import
    - Switch to branch 2024 to see Lab files. (Branches - 2024)
3. Go to Pipelines, and then select **Create pipeline** if creating your first pipeline.
4. Choose **Azure Repos Git** for the source of your code
5. Select your repository
6. Choose **Starter pipeline**
7. In the loaded yaml comment line 10  
8. Line 9 should look like this: `pool: self-hosted`

> :memo: Remember, we need to run at least one agent available to run our pipeline and in our case it will be the one created by us, this is the only option as Microsoft ones are not provided yet.

9. Hit save and run on the right-side and leave the selected option to *commit directly to master branch*.
   If you see permit request for the pipeline to access the pool please grant it.
10. Check pipeline run results by selecting the pipeline.

    *Questions:* 
    How many stages the pipeline has? What about jobs?
    On which agent it ran?
    Can you explain the checkout step? Why is it needed?

11. Let's add a parameter for the image pool that will contain 2 values: `windows-latest` and `ubuntu-latest`.
   - Go to **Repos - Files** and you should see your pipeline file - **azure-pipelines.yml**
   - Edit **azure-pipelines.yml** and add the code required for the vmimage parameter. You can name it however you want.
   - Leave **commit changes directly to main branch** and hit commit.
   (*commit* or *branch* are git actions and don't worry if you are not familiar with them yet) -->
12. Run again the pipeline. We should see the vmimage parameter selection.

    *Question:* What happend with the pipeline after commit message was completed?

13. Next, **remove** all the lines starting with *steps* block from **azure-pipelines.yml** file and replace it with all the content from **variables-sample.yml**.

    *Questions:*
    Did we had to run again manually the pipeline?
    What was the value of variable *devschool* in all the tasks? Did it changed? 

14. Explore some system variables, remember their utility?
    * add new **script task** which will output following system variables values `$(System.DefaultWorkingDirectory) , $(Pipeline.Workspace), $(Build.ArtifactStagingDirectory)` 
    * as a bonus, inside same script block add the command to see folders content:
    `ls -R $(System.DefaultWorkingDirectory) $(Pipeline.Workspace) $(Build.ArtifactStagingDirectory) `

15. **Publish an artifact**. Remember that artifacts are collection of files needed for your deployment.
    - Go to **Pipelines** menu and select your pipeline.
    - Edit button in the right
    - We will have our pipeline yaml opened in edit mode with tasks assistant panel on the right
    - Add one empty line at the end of your pipeline yaml
    - Now, in tasks panel search for *publish pipeline* task and select
    - Complete the properties of the publish task as follow:
        * file or directory path: `$(System.DefaultWorkingDirectory)`
        * artifact name: `first_artifact`
    - Rest of the properties leave unchanged
    - Add task and validate and save
    - Pipeline should trigger automatically
    - Artifact should be visible by selecting the last pipeline run.
    - Check artifact content

