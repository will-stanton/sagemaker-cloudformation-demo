# Sagemaker Endpoint CloudFormation Demo
This is a simple example of using GitHub Actions and AWS CloudFormation to deploy a pre-trained AWS Sagemaker model as an API endpoint. The GitHub Actions workflow uses the marketplace action `aws-actions/configure-aws-credentials` to authenticate to AWS and uses the AWS CLI to deploy the CloudFormation template. The CloudFormation template is based on [an example from the AWS documentation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-sagemaker-model.html), altered to use different parameters and to work with a built-in Sagemaker model.

## Training a Model

The model for this demo is an `xgboost` model trained using a Sagemaker Jumpstart demo notebook. You can find plenty of examples of these in Sagemaker Studio. One note: if you used a Sagemaker built-in, you need to specify a `ModelDataUrl` in the container definition. If you are training your own model, you do not need to specify `ModelDataUrl`.

## Setting up your AWS Account

Note: This project requires an AWS account. Some of this does *not* use the free tier, so beware! 

You will need an AWS account and a Sagemaker domain. 

You will also need IAM permissions set up properly. One simple way (which is OK for a demo but should be replaced by an OIDC integration in the enterprise) is to create a *new* IAM user (*not* the root user of the account!) with the appropriate IAM policies attached, and use GitHub Actions Secrets to store AWS access and secret keys. *NEVER PUT YOUR AWS SECRET AND ACCESS KEYS IN YOUR CODE OR ON GITHUB* 

The user or role that GitHub Actions runs as will need permissions to interact with Sagemaker and CloudFormation. For example you can use the following AWS Managed Policies:

- AmazonSageMakerFullAccess	
- AWSCloudFormationFullAccess

AWS will also create a Sagemaker Execution Role when you set up your Sagemaker domain. You will need to reference the `arn` for this in the CloudFormation stack. If you use this GitHub Action, you can set this `arn` in GitHub Actions Secrets.

## Running the GitHub Action

This is set up with a _workflow action_, which means that you can navigate to the Actions tab in your repo to manually trigger the action.



