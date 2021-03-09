# Lab-Bring-your-own-custom-container-with-Amazon-SageMaker

**Prerequisites**:
First you need to start by adding additional policies to your existing Sagemaker execution role, which allow SageMaker Studio to create a repository in Amazon ECR with the prefix smstudio, and grant permissions to push and pull images from this repo. To use an existing repository, replace the Resource with the ARN of your repository. To create a repository in Amazon ECR, SageMaker Studio uses AWS CodeBuild, and you also need to include the CodeBuild permissions shown below for more detials see here: (https://aws.amazon.com/blogs/machine-learning/bringing-your-own-custom-container-image-to-amazon-sagemaker-studio-notebooks/).

