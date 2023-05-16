# Final-Project-Assessment-for-Scalefocus-Academy
### Deploy a WordPress on Kubernetes with Helm and automation with Jenkins
# Prerequisites:
### Before getting started, make sure you have the following tools installed:
### Kubernetes
### Helm
### Jenkins
# Getting Started
### Follow these steps to deploy WordPress on Kubernetes using Helm and Jenkins:
### Open the Jenkins dashboard and create a new pipeline project.
### Configure the pipeline to use the Jenkinsfile included in this repository.
### Set up the necessary credentials in Jenkins to access your GitHub repository.
### Check if the wp namespace exists. If it doesn't, the pipeline will create it automatically.
### Check if the WordPress deployment already exists in the wp namespace. If it doesn't, the pipeline will install the Helm chart.
### Verify that the Helm deployment was successful and the WordPress pods are running.
### Access the WordPress site by loading the home page and verify that it's working correctly.
# Repository Structure:
![Screenshot_5](https://github.com/zarkoPP/Final-Project-Assessment-for-Scalefocus-Academy/assets/83474116/9c0fd7f5-ccbc-436c-807d-9cc604293c5b)
# Additional Information
### In order to install the Kubernetes, Helm and the Jenkins please follow the official guidelines.
###
### Changing the Jenkins configuration to read from the repository:
![Screenshot_1](https://github.com/zarkoPP/Final-Project-Assessment-for-Scalefocus-Academy/assets/83474116/4f991c3f-343a-4b62-95d6-6f6a8857bc9c)

### We have build success:
![Screenshot_2](https://github.com/zarkoPP/Final-Project-Assessment-for-Scalefocus-Academy/assets/83474116/1906462d-6749-4022-8312-41e141bff42c)
### Check the pods state:
![Screenshot_6](https://github.com/zarkoPP/Final-Project-Assessment-for-Scalefocus-Academy/assets/83474116/2cd5aff9-eb9b-45a2-8a2b-a313dedb366a)
### After the build succeded we gonna have to forward the port from the host to the pod:
![Screenshot_4](https://github.com/zarkoPP/Final-Project-Assessment-for-Scalefocus-Academy/assets/83474116/91ca3e5d-d825-4b38-8a8d-7df814223e84)
### And we get working website hosted on kubernetes:
![Screenshot_3](https://github.com/zarkoPP/Final-Project-Assessment-for-Scalefocus-Academy/assets/83474116/0b5a3b4a-073a-4e7a-80a7-f32e09a3feb2)
