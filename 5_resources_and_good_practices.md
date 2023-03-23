# Resources

Resources are a way to connect pipelines together in more complex flows and scenarios. 

In resources you can have pipelines, builds, repositories, containers, packages, and webhooks, and this gives you access to them through the pipeline with all their outputs.

> This is really important because it makes complex flows and logic possible on multiple repos and pipelines.

Start learning/reading from here: https://learn.microsoft.com/en-us/azure/devops/pipelines/process/resources?view=azure-devops&tabs=schema 

# Good practices

* Organize everything before starting a project - repos, templates, resources to make your life easier
* Split functionality into templates (this will help you reuse pieces of code)
* Split templates across repos for added security and centralizing work (in teams)
* Use conditions, dependencies and conditionals to minimize your code complexity and length
* Use logic and templates combined to reuse as much as possible and input/output variables as contexts needs them
* Use the GUI for task examples and help with your YAML formatting
* Last but not least "Smile and be happy!"