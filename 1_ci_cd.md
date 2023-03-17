# CICD

> Code -> Build -> Test -> Release -> Deploy -> Operate -> Monitor -> Plan
> 
> Repeat :)

In short, CI/CD is the continuous process that covers the cycles of a software product.

Azure DevOps like GitLab, Jenkins and many others is a CI CD tool to facilitate your DevOps operations.

## Orchestration
The common approach in modern CICD is to have an orchestrator that you give instructions to. The definition of this instructions is the pipeline itself. 

The pipeline is picked up by agents that run your pipeline. This way you can orchestrate multiple pipelines that can depend or not on eachother and resolve complex tasks and flows using one or more agents that run the instructions you write.

## Agents
Agents or runners actually run your instructions. Builds, installs, tests, everything is prepared and run at the agent level, to be deployed to the destination machines.

But What is an agent?
A computer that reads and runs your instructions. Depending on your needs, this computer can be equiped with a specific OS, package etc. to best do the jobs intended.

## Destination / Target machines
The place where you deploy. Physical machines or cloud, this is the place from where your application is running and is exposed to a customer.

## CiCD as code
The good practice when working with pipelines is to manage them as code versus GUI.

The benefits for this approach are:
* maintainability
* versioning control
* templating 
* usability, reusability and repurpose
* movability (you can always move code between projects)

# Azure DevOps specifics

## Agent pools
Agent pools are collection of agents grouped by OS or other criteria that you would need.

Therefore when running a pipeline you can choose a specific agent or an agent pool for your run(s)

Fpr example his are common by default pools that you can use right away:
* windows-latest
* ubuntu-latest
* macOS-latest

Agents can be Microsoft agents or Self-Hosted. The Microsoft agents are maintained by Microsoft and Self-Hosted are agents you create.

## Agent capabilities
What exactly can the agent do. You can update agents or manage their capabilities.

## Pipeline structure

    name: (optional - if you do not assign a value, it will be named by the system)

    trigger: (optional)

    schedules: (optional)

    resources: (optional)

    parameters: (optional)

    variables: (optional)

    stages: (required at least one)

        jobs: (optional - if you have only one set of steps you can ignore the jobs directive, otherwise is required)

            <steps> (required)

                task: (required)

## Parallelism and limitations
Each job is assigned to an agent. If jobs have relationships or dependencies, this needs to be specifically stated.

Depending on the context run, you can organize your runs as sequential or parallel, taking into account your agents capabilities.