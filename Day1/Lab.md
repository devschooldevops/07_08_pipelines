Starter - pipeline lab

1. Sign in to your Azure DevOps organization and go to your project.
2. Go to Pipelines, and then select New pipeline or Create pipeline if creating your first pipeline.
3. Choose Azure Repo Git for the source of your code
4. Select your new repository
5. Choose Starter pipeline

!Questions: 
     - What do you see? 
     - Is this pipeline structure familiar to you?

6. Hit save and run on the right-side.
7. Check pipeline run

!Questions: 
    - How many stages the pipeline has? What about jobs?
    - On which agent it ran?
    - Can you explain the checkout step? Why is it needed?

8. Let's add a parameter for the image pool that will contain 2 values: windows-latest and ubuntu-latest.
9. Run the pipeline again by selecting each pool. Did it worked?

Moving to a multistage pipeline. 
Objective: Using Azure Pipelines to deploy
**Prerequisites**:
1. Azure Student subcription: https://azure.microsoft.com/en-us/free/students
2

It's nice that we saw a simple pipeline, but this is not the real world :), in fact things are gonna become more interresting.
1. Let's import a new repository this time containing an
