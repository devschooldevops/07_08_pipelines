# Conditionals

Most commonly, Azure DevOps offers the "condition:" and "dependsOn:" statement in stages.

The condition needs to be met in order for the instructions below to be run, and in case of dependency, this controls if a previous task has the desired outcome, then the block will run.

> The order in which those statements are evaluated if both present is condition and after dependsOn!

Start learning/reading from here: https://learn.microsoft.com/en-us/azure/devops/pipelines/process/conditions?view=azure-devops&tabs=yaml%2Cstages 

Conditions can be specified at the stage level with the condition statement, or otherwise almost anywhere using conditions (if clauses) and indentation of the below code:

> ${{ if ne(variables['Build.SourceBranch'], 'refs/heads/master') }}:
>  [indentation] - task definition

While in condition statements you will have something like:

> condition: ne(variables['Build.SourceBranch'], 'refs/heads/master')

dependsOn: directive refers to previous stages -> more info on condition: and dependsOn: https://learn.microsoft.com/en-us/azure/devops/pipelines/process/stages?view=azure-devops&tabs=yaml 


> EXTRA
> For iterating through objects we can use the foreach statement that you previously saw at any level(task,job, stage):
> ${{ each ev in parameters.env }}: