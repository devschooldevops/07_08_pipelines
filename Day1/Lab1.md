**Starter - pipeline lab**

1. Sign in to your Azure DevOps organization and go to your project.
2. Go to Pipelines, and then select New pipeline or Create pipeline if creating your first pipeline.
3. Choose Azure Repo Git for the source of your code
4. Select your new repository
5. Choose Starter pipeline

*Questions*: 
    - What do you see? 
    - Is this pipeline structure familiar to you?

6. Hit save and run on the right-side.
7. Check pipeline run results

*Questions:* 
    - How many stages the pipeline has? What about jobs?
    - On which agent it ran?
    - Can you explain the checkout step? Why is it needed?

8. Let's add a parameter for the image pool that will contain 2 values: windows-latest and ubuntu-latest.
   - Go to Repos - Files and you should see your pipeline file - azure-pipelines.yml
   - Edit and add the code required for the vmimage parameter. You can name it how you want.
   - Commit the change to master branch.
9. Run again the pipeline. We should see the vmimage parameter selection.
*Question:* What happend with the pipeline after commit message was completed?

10. Next, remove entire *steps* block from azure-pipelines.yml file and replace it with all the content from *variables-sample.yml*
*Questions:*
   - Did we had to run again manually the pipeline?
   - What was the value of variable *devschool* in all the tasks? Did it changed? 

Let's discuss together this exercise.