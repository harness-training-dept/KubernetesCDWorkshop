# Kubernetes Continuous Deliver Workshop Labs

## Lab 1 - Login to app.harness.io and familiarize yourself with the environment


1. Load up your Chrome web browser and login to https://app.harness.io with the username and password from your lab sheet. 

2. Click around and explore the GUI. Please note depending on the user role you have in your own organization's Harness implementation you may not have access to the menus and settings you see here in our training setup. 

5. We will be visiting the Setup menu most often. Click in there and explore the different connectors and setting options. 

6. Ask your instructor if you don't understand the use of any configuration or dashboard.

## Lab 2 - Setup a basic Nginx deployment on our training cluster

1. Click on the Setup menu in the upper right hand corner of the Harness GUI.

2. Click on the Add Application button and fill out the information for your new application. Be sure to use your student ID in the name of your application so you can find it easily later.

![Application Setup](/images/application.jpg)

3. Click submit and Harness will create your new application. Now we can setup the other parts of the deployment.

4. Click on Services to add our first service to this application, then click on the Add Service button. Give your service a name that includes your student ID (as you did with the application) and set the Deployment Type to Kubernetes.

![Add Service](/images/add_service.jpg)

Click submit. That will take you to the Service Overview.

5. In the Service Overview screen click on Add Artifact Source and select Docker Registry. For Source Server select Harness Docker Hub. This is a sample connection to the public hub.docker.com domain setup automatically for harness.io. In non-training testing environments you would most likely delete this connector. For the Docker image name put library/nginx . That will allow us to pick our nginx version when we deploy.

![Artifact Source](/images/artifact_source.jpg)

Click submit when done. We won't be changing any of the preconfigured yaml at this time. We're just doing a simple first deployment. 

6. Click on your application name in the popcorn trail on the upper left of the Harness UI to return to your Application main screen. Then click on Environments to setup an environment to deploy to. 

7. Click Add Environment button and give your environment a name that starts with your student ID. Set the environment type to non-production.

![Environment](/images/environment.jpg)

When you click submit that will take you to the Environment Overview screen. 

8. Add an Infrastructure Definition. Give it a name that starts with your student ID. Select Kubernetes Cluster for your Cloud Provider Type, and set the deployment type to Kubernetes. Then you can select the Cloud Provider we have setup for this workshop. It will include the name of the city or state the workshop is held in. Finally for Namespace please put your Student ID so your instructor can see your deployment from the command line easily. 

![Infrastructure Definition](/images/infra_def.jpg)

Click submit when done. 

9. Click back on your application name in the popcorn trail and then click on Workflows. Click Add Workflow.

10. Give your workflow a name that starts with your Student ID. Select rolling deployment for your Deployment Type. Then for Environment, Service, and Infrastructure Definition be sure to pick the ones that start with your Student ID.

![Workflow](/images/workflow.jpg)

