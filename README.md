# Cab Ride Demand Prediction

This project focuses on predicting the demand for cab rides for Meiro Mobility. By analyzing various factors such as time, location, and trip duration, I aim to build an accurate model that can provide insights into the expected demand for cab services.

## Project Description

The project is divided into two main parts: feature engineering and model development. In the feature engineering phase, I explore different factors that can influence cab ride demand and devise effective methods to incorporate them into our predictive model. The model development phase involves selecting appropriate algorithms, training the model, and evaluating its performance to ensure accurate demand predictions.

## Feature Engineering

I used 2 approaches for calculating demand both are described below as problem and solution.

### Problem Statement
The initial approach of considering only the number of active drivers within fixed time intervals proved insufficient to capture the true demand dynamics. I faced challenges in understanding the spatial distribution of demand and accounting for the varying factors affecting different regions within the service area.

### Solution

To address these challenges, I employed a data-driven approach for feature engineering:

1) **Spatial Analysis**: I leveraged KMeans Clustering to divide the service area into clusters or zones, identifying areas with high cab ride demand. This allowed me to calculate how many cab rides were active in a particular zone in 15 minute time interval as demand (Higher the number of cab rides in an area higher the demand). I used within-cluster sum of squares algorithm and knowledge of total area of Ahemdabad to calculate optimum amount of zones (Here 50). Each zone represents an area of 10km square approximately.

![image](https://github.com/Kranium2002/meiro_task/assets/74452705/248456c7-3c5c-49db-9ef9-500a88efca11)


2) **Temporal Analysis**: I considered time-based features such as hour of the day, day of the week, and month and selected the best features from them using SelectKBest from SKLearn.
   
3) **Trip Duration and Distance**: By incorporating pre-calculated trip duration (assuming that trip duration is pre calculated) and distance, I accounted for the travel time and distance covered during each ride, which are essential factors influencing demand.

## Models Used and Accuracy

I explored different modeling techniques to predict cab ride demand and evaluated their accuracy using appropriate metrics:

1) **XGBoost**: I employed the XGBoost algorithm to train a predictive model for cab ride demand. This gradient boosting technique proved effective in capturing complex relationships between features and demand patterns. The XGBoost model achieved an MSE of 0.26661763 and an accuracy of 0.9464550029603316, making it a strong performer.

2) **Logistic Regression**: Although logistic regression is a popular model for classification tasks, it failed to converge for my demand prediction problem. The complexity of the data and its non-linear nature may have contributed to this outcome.

3) **Feedforward Neural Network**: I built a feedforward neural network model using the Keras library. This deep learning model exhibited promising results with a loss (MSE) of 0.11856061220169067 and an accuracy of 0.9181098341941833.

![image](https://github.com/Kranium2002/meiro_task/assets/74452705/43f9eefd-244a-4cdf-978d-676735a381aa)


### Best Model

While the XGBoost model demonstrated superior accuracy, the neural network model exhibited lower loss, indicating its potential for capturing more intricate demand patterns. Further experimentation and analysis can help determine the most suitable model for specific scenarios.

## Deployment Steps (This is a very high level design for deployment system)

1. **Choose the Model Architecture**:
   - Select a suitable architecture for cab ride demand prediction, such as a feedforward neural network or a gradient boosting machine.

2. **Set Up AWS Infrastructure**:
   - Create an AWS account if you don't have one already.
   - Set up Amazon EC2 instances to host the prediction model.
   - Utilize Amazon Elastic Load Balancer to distribute incoming requests across multiple instances.
   - Configure Amazon RDS or DynamoDB for data storage.

3. **Develop the Prediction API**:
   - Use a lightweight web framework like Flask, Fast API or Django to develop a RESTful API for handling prediction requests.
   - Implement the prediction logic using the selected model architecture.

4. **Capture Real-Time Ride Data**:
   - Utilize Amazon Kinesis to capture real-time ride data from various sources.
   - Set up data streaming pipelines to ingest data into the system.

5. **Store Captured Data**:
   - Choose an appropriate AWS storage service like Amazon S3 to store the captured ride data.
   - Design the data schema and organize the data in a way that facilitates retraining.

6. **Set Up Retraining Pipeline**:
   - Use AWS Lambda functions a retraining pipeline based on a defined schedule or after a specific number of ride data points.
   - Retrieve the relevant data from Amazon S3, preprocess it, and train a new model using Amazon SageMaker.

7. **Manage Model Versions**:
   - Utilize Amazon SageMaker for model versioning, deployment, and A/B testing.
   - Implement a mechanism to seamlessly switch between different model versions during deployment.

8. **Monitor and Alert**:
   - Utilize AWS CloudWatch to monitor various metrics such as latency, throughput, and EC2 instance health.

9. **Implement CI/CD Pipeline**:
   - Use AWS CodePipeline to automate the CI/CD process.
   - Set up a continuous integration and deployment pipeline for smooth updates and releases.

## More Info

Please refer to the notebook file for detailed documentation and explanations of each step.
