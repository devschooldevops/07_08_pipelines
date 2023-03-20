# Parameters

Parameters are user input values. Those influence your pipeline runs and behaviour.

Parameters are defined within the "parameters:" directive and are used commonly as {{parameters.ParameterName}} 

> Parameters are only available at template parsing time. Parameters are expanded just before the pipeline runs so that values surrounded by ${{ }} are replaced with parameter values. 

From the above statement we can understand that we can not template parameters!  

Start learning/reading from here: https://learn.microsoft.com/en-us/azure/devops/pipelines/process/runtime-parameters?view=azure-devops&tabs=script 

Instructions (let's get familiar with parameters):
 
* Complete the code echo "My name is "
* Create a new parameter definition
* Use different types of parameters and test the outcome (string, boolean, object)
* Try to use the new paramethers in the tasks of the pipeline
* Echo a boolean parmeter (surprise inside)