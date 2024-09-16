# Lab2 - Multistage pipeline

## In this lab we will build and deploy a Python application to Azure App Services (WebApp)

> Azure App Service is an HTTP-based service for hosting web applications, REST APIs, and mobile back ends. 
> You can develop in your favorite language, be it .NET, .NET Core, > Java, Node.js, PHP, or Python. Applications run and scale with ease on both Windows and Linux-based environments.


*Don't worry if you are not familiar with python, we will not dive into code.*
*This lab is focusing on exercise part having in mind that it was followed the process to open an Azure Student Subscription under same account of Azure Devops*

So, let's have some real fun :)

1. Open your Devops Organization and go to Repos.
2. Import repository with URL: `https://github.com/Azure-Samples/msdocs-python-flask-webapp-quickstart`
3. After import was successfull have a general view on the source code files.
4. Our application is missing an automated way to be deployed, so Azure Pipelines is required here.
5. From previous lab repo download **python-pipeline.yml** file
5. Switch to the newly imported repo (should be **msdocs-python-flask-webapp-quickstart**) if the name was not changed at import
6. Click on right side ... menu and choose **Upload file(s)** 
7. Upload the downloaded **python-pipeline.yml** and hit `Commit`.

** Now we have a pipeline, but does it work? **
Let's find together what is missing.