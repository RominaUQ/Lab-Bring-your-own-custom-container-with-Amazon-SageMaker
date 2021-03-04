# Lab-Bring-your-own-custom-container-with-Amazon-SageMaker

**Prerequisites**:
First you need to start by adding additional policies to your existing Sagemaker execution role, which allow SageMaker Studio to create a repository in Amazon ECR with the prefix smstudio, and grant permissions to push and pull images from this repo. To use an existing repository, replace the Resource with the ARN of your repository. To create a repository in Amazon ECR, SageMaker Studio uses AWS CodeBuild, and you also need to include the CodeBuild permissions shown below for more detials see here: (https://aws.amazon.com/blogs/machine-learning/bringing-your-own-custom-container-image-to-amazon-sagemaker-studio-notebooks/).

{
            "Effect": "Allow",
            "Action": [
                "ecr:CreateRepository",
                "ecr:BatchGetImage",
                "ecr:CompleteLayerUpload",
                "ecr:DescribeImages",
                "ecr:DescribeRepositories",
                "ecr:UploadLayerPart",
                "ecr:ListImages",
                "ecr:InitiateLayerUpload",
                "ecr:BatchCheckLayerAvailability",
                "ecr:GetDownloadUrlForLayer",
                "ecr:PutImage"
            ],
            "Resource": "arn:aws:ecr:*:*:repository/smstudio*"
        },
        {
            "Effect": "Allow",
            "Action": "ecr:GetAuthorizationToken",
            "Resource": "*"
           }
{
            "Effect": "Allow",
            "Action": [
                "codebuild:DeleteProject",
                "codebuild:CreateProject",
                "codebuild:BatchGetBuilds",
                "codebuild:StartBuild"
            ],
            "Resource": "arn:aws:codebuild:*:*:project/sagemaker-studio*"
}
{
            "Effect": "Allow",
            "Action": "iam:PassRole",
            "Resource": "arn:aws:iam::*:role/*",
            "Condition": {
                "StringLikeIfExists": {
                    "iam:PassedToService": "codebuild.amazonaws.com"
                }
            }
        }
        
        
Your SageMaker role should also have a trust policy with AWS CodeBuild as shown below. For more information, see Using the Amazon SageMaker Studio Image Build CLI to build container images from your Studio notebooks
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": [
          "codebuild.amazonaws.com"
        ]
      },
      "Action": "sts:AssumeRole"
    }
  ]
}   
