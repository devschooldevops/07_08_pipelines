# Templates

Templates are parts of a pipeline that can be easily reused in the same context (pipeline) or in different pipelines as well.

Templates can be generated:
* at a stage level
* at a job level
* at a task level

Templates link to the main pipeline with parameters. At the template level we define and use parameters, but the value of those parameters in the main pipeline can be anything from other parameters, variables or conditionals.

When to use templates?
* when a sequence of code is repeated with different inputs
* when you need to separate functional templates
* when you need to reuse parts of a pipeline in another pipeline or flow

> EXTRA:
> Templates can be a means of securing your pipeline by moving critical instructions in a template, in another protected repo and so on. 
> This means that only people who have access to that repo can alter the functionality of your pipeline.