## Overview
In this project, we go through the various tasks and steps to operationalize Machine Learning Pipeline in Azure. The steps involved are:

1. Authentication
2. Defining your Machine Learning Model
3. Defining your Compute Infrastructure
3. Deploying the Model
4. Logging and enabling application insights for better troubleshooting
5. Consuming Model Endpoints
6. Creating pipeline to automate the whole process


##Architectural Diagram




##How to improve the project in the future



##Tasks/Topics Covered:


###Authentication

In this task, we create a service principal **ml-auth** and give the service princpal the role of owner:

- Ensure az is installed in the system, use az login to login to azure
```
az login
```
- Make sure az extension:  **azure-cli-ml** for machine learning is installed
```
az extension add -n azure-cli-ml

```
- Create a service principal with the name of **ml-auth**
```
az ad sp create-for-rbac --sdk-auth --name ml-auth

```
- Get the object Id of the service principal from the client-id of the service principal using the below command
```
az ad sp show --id xxxxxxxx-aea4-401c-a66e-xxxxxxxxxxxx
```
- Use the object Id from above to assign a role to the service principal, we are assigning the role of "owner" in the example below:
```
az ml workspace share -w azure-ml-nd-ws -g azure-ml-nd --user xxxxxxxx-5a2a-4309-bb06-xxxxxxxxxxxx --role owner
```





![authentication](./images/authentication.png)


###AutoML Experiment

In this task, we create a new Automated ML run: Steps involved are as below:

- Select the dataset available(we have Bank-marketing dataset from the previous project) or create a new dataset.
- Select the compute cluster or create a new cluster
- Use an existing experiment or create a new experiment
- Choose the Target column, we use the column 'y' for our run
- Select the task type, in our case it is classification.

Dataset Used:

![dataset](./images/dataset.png)

Experiment Run:

![experiment1 completed](./images/experiment1_completed.png)

Best Model of the run: VotingEnsemble

![best model](./images/best_model.png)


###Deploying the Model

Follow the following steps to deploy the model:

- Choose the best model from the **Models** tab of the experiment. The best model will be at the top of all the models.
- Click "Deploy" to deploy the model.
- Name the deployment, and choose the compute type. We have used the compute type as Azure Container Service and enabled authentication.

Deployment can be visible in Endpoints:
![deployment](./images/deployment.png)

###Logging and enabling application insights

Follow the following steps to see logs for the endpoint and to enable application insights:

- Download the config.json from the azure workspace
- Update the logs.py file with the name of the deployement, and update the attribute **enable_app_insights = True** for the Webservice.
- Run logs.py to see the logs 
```
python logs.py

```
Logs:
![logs](./images/logs.png)

Application Insights enabled:
![app insights](./images/app_insights.png)

###Swagger Documentation

###Consuimg Model Endpoints

### Create, Publish and Consume a Pipeline










