# Operationalizing Machine Learning
This project is part of the Udacity Azure ML Nanodegree. In this project we configure a Machine Learning model, deploy it and consume it. Finally a pipeline is created, published and consumed. The dataset used contains bank marketing data pertaining to 32950 people. The machine learning model predicts if a client will subscribe to the service or not. The prediction is based on several parameters including age of the customer, their marital status, the campaign number, loan status, their education details, etc. AutoML has been used to find the best model for this problem.

## Architectural Diagram
The whole process of configuring the model, deploying it and consuming it can be understood by the following diagram- 
![Architecture Diagram](https://github.com/neha7598/azure-ml-project2/blob/main/Screenshots/Architecture.png)


**1. Configure Model**
- Register Dataset- The Bank Marketing data set was obtained from [here](https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv) and uploaded to Azure Machine Learning Studio.
- AutoMl Run- An AutoML run was configured using the Bank Marketing data.
- Select Best Model- Best model from the AutoML run was selected for deployment. In this case the best Model was the Voting Ensemble model with an accuracy of 92.049%

**2. Deploy Model**
- Deploy model using Azure Container Instance (ACI)
- Enable Authentication
- Enable Application Insights- Application Insights were enable through code using the [logs.py](https://github.com/neha7598/azure-ml-project2/blob/main/logs.py) file 
- Swagger Documentation- Swagger is a tool that eases the documentation efforts of HTTP APIs. To make it available on localhost files in the [swagger directory](https://github.com/neha7598/azure-ml-project2/tree/main/swagger) were executed.

**3. Consume Model**
- Publish model using the REST endpoint provided by azure
- Authenticate using primary key
- Interact with model using [endpoint.py](https://github.com/neha7598/azure-ml-project2/blob/main/endpoint.py)- 2 sets of data are passed to the model and the result is obtained as JSON.  

## Key Steps
The following steps were carried out as part of the project- 

### 1. Authentication
As part of this step a Service Principal account needs to be created and associated with the current workspace. SInce all work was carried out in the project Lab this step was not carried out due to lack of permissions. 

### 2. Automated ML Experiment
In this step an AutoML Run was initialised using the Bankmarketing dataset which was uploaded to the Azure Machine Learning Studio. A new compute cluster was configured amd the experiment was run using *Classification*. The best model which in this case was Voting Ensemble (accuracy 92.049%), was selected.

**Screenshot of Registered Dataset in ML Studio**
![Registered Dataset](https://github.com/neha7598/azure-ml-project2/blob/main/Screenshots/1-Registered%20Dataset.png)

**Screenshot showing Experiment as Completed**
![Experiment Completed](https://github.com/neha7598/azure-ml-project2/blob/main/Screenshots/1-Experiment%20Completed.png)

**Screenshot of Best Model**
![Best Model](https://github.com/neha7598/azure-ml-project2/blob/main/Screenshots/1-Best%20Model.png)

### 3. Deploying the Best Model
As part of this step the best model (i.e. Voting Ensemble) was deployed using Azure Container Instance (ACI).

### 4. Enable Application Insights
In this step Application Insights were enabled for the deployed model using the logs.py file by the following line of code-
```
service.update(enable_app_insights =True)
```
Then logs were generated

**Screenshot showing Application Insights are enabled**
![Application Insights](https://github.com/neha7598/azure-ml-project2/blob/main/Screenshots/3-Application%20Insights%20Enabled.png)

**Screenshot showing logs generated**
![Logs](https://github.com/neha7598/azure-ml-project2/blob/main/Screenshots/3-Running%20logs.png)

### 5. Swagger Documentation
In this step the swagger documentation for the deployed model is made available on localhost and we interact with the swagger instance running with the documentation for the HTTP API of the model

**Screenshot  showing swagger runs on localhost**
![Swagger Documentation](https://github.com/neha7598/azure-ml-project2/blob/main/Screenshots/4-Swagger%20on%20localhost.png)
![Swagger Documentation cont](https://github.com/neha7598/azure-ml-project2/blob/main/Screenshots/4-Swagger%202.png)

### 6. Consume Model Endpoint
In this step we consume the deployed model and interact with it using the REST endpoint and the primary key by running endpoint.py. 2 sets of data are passed to the model and a result is obtained for each as JSON. A data.json file is also created in the current working directory. After that the model's performance is Benchmarked using Apache Benchmark tool.

**Screenshot of produced JSON output from model**
![JSON OUtput](https://github.com/neha7598/azure-ml-project2/blob/main/Screenshots/5-Json%20output.png)

**Screenshot showing Apache Benchmark runs against the HTTP API**
![Benchmark](https://github.com/neha7598/azure-ml-project2/blob/main/Screenshots/5-Benchmark%201.png)
![Benchmark2](https://github.com/neha7598/azure-ml-project2/blob/main/Screenshots/5-Benchmark%202.png)

### 7. Create, Publish and Consume a Pipeline
In this step we create, publish and consume a pipeline through the provided Jupyter Notebook.

**Screenshot showing the pipeline section of Azure ML Studio with the created Pipeline**
![Pipeline Created](https://github.com/neha7598/azure-ml-project2/blob/main/Screenshots/6-Pipeline%20created.png)

**Screenshot of Pipeline Section showing Pipeline endpoint**
![Pipeline Endpoint](https://github.com/neha7598/azure-ml-project2/blob/main/Screenshots/6-Pipeline%20Section-%20Pipeline%20Endpoints.png)

**Screenshot of the Bankmarketing Dataset with AutoML module**
![Bankmarketing dataset with AutoML Module](https://github.com/neha7598/azure-ml-project2/blob/main/Screenshots/6-BankMarketing%20with%20AutoML%20module.png)

**Screenshot of Published Pipeline Overview, showing a REST endpoint and status of Active**
![Published Pipeline Overview](https://github.com/neha7598/azure-ml-project2/blob/main/Screenshots/6-Published%20Pipeline%20Overview.png)

**Screenshot showing Run Details widget**
![Run Details](https://github.com/neha7598/azure-ml-project2/blob/main/Screenshots/6-Run%20Details%20Widget.png)

**Screenshot of ML Studio showing scheduled run**
![Run](https://github.com/neha7598/azure-ml-project2/blob/main/Screenshots/6-ML%20Studio%20showing%20sheduled%20Runs.png)


## Future Improvements
Future experiments can explore having a experiment timeout time of more than 20 minutes, this can lead to a more exhaustive search and potentially better results. Also the class imbalance detected by AUTOML can be worked on by using different undersampling or oversampling techniques. Synthetic Minority Oversampling Technique (SMOTE) could also be used. We can also improve the project to carry out all the steps like enabling Application Insights, Swagger Documentation from the Jupyter Notebook itself. Thus the entire project can be executed from the Jupyter Notebook instead along pipeline creation, publication and consumption. 
