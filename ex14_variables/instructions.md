# Variables

Variables help you move data and use data in your pipelines. Generally variables are things you have and are needed for your flows. In this sense you can template easily variables and use them from separate sources. 

Variables are defined within the "variables:" directive.

There are 2 main types of variables:
* User defined variables
* Predefined variables (those make your life easier, and are available for your information here: https://learn.microsoft.com/en-us/azure/devops/pipelines/build/variables?view=azure-devops&tabs=yaml )

>The main use of variables, after their definition is like this "$(VariableName)" if the variable needs to be considered as a runtime requirement (it contains a webhook, an endpoint a service connection etc.) then we will call the variable like this "${{variables.VariableName}}

Instructions (let's get familiar with variables):

* create 2 new variables and use them
* check the predefined variables and echo 2 of them
* use this command inside one of the tasks: echo "##vso[task.setvariable variable=myVariable;issecret=true]secretvalue"
* echo $(myVariable)
* finally let's talk about "vso" tasks (together, not alone but as a good starter you can also open this page: https://learn.microsoft.com/en-us/azure/devops/pipelines/process/set-variables-scripts?view=azure-devops&tabs=bash )