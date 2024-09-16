**Starter - pipeline lab**

1. Sign in to your Azure DevOps organization (https://dev.azure.com/[organization]) and go to your project.
2. Go to Pipelines, and then select **New pipeline** or Create pipeline if creating your first pipeline.
3. Choose **Azure Repo Git** for the source of your code
4. Select your new repository
5. Choose **Starter pipeline**

    *Questions*: 
    What do you see next? 
    Is this pipeline structure familiar to you?


6. Hit save and run on the right-side.
7. Check pipeline run results by selecting the pipeline

    *Questions:* 
    How many stages the pipeline has? What about jobs?
    On which agent it ran?
    Can you explain the checkout step? Why is it needed?

8. Let's add a parameter for the image pool that will contain 2 values: `windows-latest` and `ubuntu-latest`.
   - Go to **Repos - Files** and you should see your pipeline file - **azure-pipelines.yml**
   - Edit **azure-pipelines.yml** and add the code required for the vmimage parameter. You can name it however you want.
   - Leave **commit changes directly to main branch** and hit commit.
   (*commit* or *branch* are git actions and don't worry if you are not familiar with them yet)
9. Run again the pipeline. We should see the vmimage parameter selection.

    *Question:* What happend with the pipeline after commit message was completed?

10. Next, **remove** all the lines starting with *steps* block from **azure-pipelines.yml** file and replace it with all the content from **variables-sample.yml**.

    *Questions:*
    Did we had to run again manually the pipeline?
    What was the value of variable *devschool* in all the tasks? Did it changed? 

11. Explore some system variables, remember their utility?
    * add new **script task** which will output following system variables values `$(System.DefaultWorkingDirectory) , $(Pipeline.Workspace), $(Build.ArtifactStagingDirectory)` 
    * as a bonus, inside same script block add the command to see folders content:
    `ls -R $(System.DefaultWorkingDirectory) $(Pipeline.Workspace) $(Build.ArtifactStagingDirectory) `

12. **Publish an artifact**. Remember that artifacts are collection of files needed for your deployment.
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

