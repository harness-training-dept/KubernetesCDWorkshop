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

When you're done. Click submit.

11. Now we are ready to do the actual deploy! Click on the Deploy button in the upper right corner of the screen. That will bring up the Start New Deployment dialog box. 

12. Since we specified "library/nginx" as our artifact source we now have to pick which version of Nginx we wish to deploy. For our first deploy select an older version 1.9.15 for example. (We will upgrade in the next lab to the current version.)

![Start New Deployment](/images/start_new.jpg)

It's a good idea for test and training deployments to select Send Notification to Me Only to avoid spamming your coworkers with test deployments. Click Submit to kick off the deployment.

13. Harness will switch to the deployment screen. Click on each box as it appears to see what information Harness provides. Click on the Rollout Deployment box to see the results from the command line on the delegate.

![Live Deployment View](/images/deployment_view.jpg)

Your instructor will also be displaying information from the actual cluster itself on the projector. Look up there to see your namespace appear once your deployment gets going. 


## Lab 3 - Upgrade your Nginx deployment to the latest version

1. Click on your application in the popcorn trail and go back to your Deployments. In there click on the Deploy button to deploy the latest version of Nginx.

![Deploy Latest](/images/deploy_latest.jpg) 

Be sure to select the most recent version of Nginx and hit submit.

2. Once the deploy starts click on the Rollout Deployment step and verify the yaml with the latest version of Nginx.

![Check Upgrade](/images/check_upgrade.jpg)

It really can be that easy to upgrade a service!

## Lab 4 - Cleanup the cluster

1. Now we can run a deployment to delete our previous deployment and leave our training cluster neat and tidy! Go back to Setup screen in the Harness UI and select your application. We're going to create a new Workflow to delete our namespace and the pod inside it. 

2. Click on Workflows and Add Workflow. Give this workflow a different name, but be sure to include your student ID.

![Cleanup Workflow](/images/clean_wf.jpg)

Click submit.

3. By default Harness put a Rollout Deployment step in for us, but we don't actually need that. Hover your mouse over the Rollout Deployment stage and click the X that appears next to that step to delete it. 

![Remove Step](/images/remove_step.jpg)

4. Once that step is gone click on Add Step. This takes you to the Workflow step creation dialog. Click on Kubernetes and then the Delete action. 

![Delete Step](/images/delete_step.jpg)

Click next.

5. Tell Harness what you want the Kubernetes delete command to delete. We will hardcode our namespace, but you could also use a variable here to Delete whatever namesapce was associated with the deployment. 

![Configure Delete](/images/configure_delete.jpg)
