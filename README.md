# Operationalizing Machine Learning
This project is part of the Udacity Azure ML Nanodegree. In this project we configure a Machine Learning model, deploy it and consume it. Finally a pipeline is created, published and consumed. The dataset used contains bank marketing data pertaining to 32950 people. The machine learning model predicts if a client will subscribe to the service or not. The prediction is based on several parameters including age of the customer, their marital status, the campaign number, loan status, their education details, etc. AutoML has been used to find the best model for this problem.

## Architectural Diagram
*TODO*: Provide an architectual diagram of the project and give an introduction of each step. An architectural diagram is an image that helps visualize the flow of operations from start to finish. In this case, it has to be related to the completed project, with its various stages that are critical to the overall flow. For example, one stage for managing models could be "using Automated ML to determine the best model". 
1. **Configure Model**
- Register Dataset- The Bank Marketing data set was obtained from [here](https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv) and uploaded to Azure Machine Learning Studio.
- AutoMl Run- An AutoML run was configured using the Bank Marketing data.
- Select Best Model- Best model from the AutoML run was selected for deployment. In this case the best Model was the Voting Ensemble model with an accuracy of 92.049%

2. **Deploy Model**
- Deploy model using Azure Container Instance (ACI)
- Enable Authentication
- Enable Application Insights- Application Insights were enable through code using the [logs.py](https://github.com/neha7598/azure-ml-project2/blob/main/logs.py) file 
- Swagger Documentation- Swagger is a tool that eases the documentation efforts of HTTP APIs. To make it available on localhost files in the [swagger directory](https://github.com/neha7598/azure-ml-project2/tree/main/swagger) were executed.

3. **Consume Model**
- Publish model using the REST endpoint provided by azure
- Authenticate using primary key
- Interact with model using [endpoint.py](https://github.com/neha7598/azure-ml-project2/blob/main/endpoint.py)- 2 sets of data are passed to the model and the result is obtained as JSON.  

## Key Steps
*TODO*: Write a short discription of the key steps. Remeber to include all the screenshots required to demonstrate key steps. 

## Screen Recording
*TODO* Provide a link to a screen recording of the project in action. Remember that the screencast should demonstrate:

## Standout Suggestions
*TODO (Optional):* This is where you can provide information about any standout suggestions that you have attempted.
