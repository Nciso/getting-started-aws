# AutoCloud Infrastructure as Code Catalog Getting Started Blueprint - Amazon Web Services



## Overview
AutoCloud Terraform Blueprints are a way for organizations to deploy consistent, well-architected patterns that meet organization standards and requirements across many teams, with less friction between application, security, and platform concerns.

This "write-once, deploy-many" strategy allows pattern architects to design, define, and maintain best practice patterns with cost, security, and compliance standards baked in, and makes them available for consumption to end users in a self-service portal. These consumers are shown a form wizard that quickly gathers the required configuration input. Upon submission, AutoCloud runs cost, security, and compliance analysis, and autogenerates Terraform code implementing the assets. This code is then submitted in a git pull request for review and deployment using your existing Terraform tooling and workflows.

The example pattern created by this blueprint addresses a very common use case for AWS users that is a frequent source of misconfiguration: the deployment of a private, KMS-encrypted S3 bucket.



## Deploying This Blueprint

### Download Code

The first step to deploying this getting started blueprint is to set up a local copy of this codebase.

If you have gone through the getting started process in AutoCloud, you have downloaded this code already, and it has been pre-configured with API access for you. You are ready for the next step.

If you are reading this on Github, you can clone this repository or [download the code here](https://github.com/autoclouddev/getting-started-aws/archive/refs/heads/main.zip).

### Configure Access Credentials

Before executing the Terraform actions to create the AutoCloud Terraform blueprint, you will need to ensure that your shell environment has been configured to authenticate to AutoCloud. Similarly, to execute the Terraform generated by the AutoCloud blueprint, you will need to configure your shell environment to authenticate to AWS.

#### AutoCloud

The AutoCloud provider requires an API token to authenticate and access the AutoCloud service. The provider is configured in the file `./provider.tf`. See the comments in that file for details on configuring AutoCloud access.

#### AWS

The AWS Terraform provider will use the authentication mechanism set up in your shell environment by default. Before you run Terraform commands, you will need to set `AWS_REGION` to the region that you want to deploy to, and either `AWS_PROFILE` or `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`:

```bash
% export AWS_REGION="us-east-1"
% export AWS_ACCESS_KEY_ID="anaccesskey"
% export AWS_SECRET_ACCESS_KEY="asecretkey"
```

Your specific configuration will depend on your organization's tooling and standards.

For more information on configuring access for the AWS provider, see the [official provider documentation](https://registry.terraform.io/providers/hashicorp/aws/latest/docs#authentication-and-configuration). 

### Run Terraform to Create Blueprint

You are now ready to deploy the Terraform blueprint. In the terminal you used to configure access in the previous step, execute the Terraform to create the IaC blueprint in AutoCloud:

```bash
% terraform init
% terraform plan
% terraform apply
```

You should see the new IaC Terraform Blueprint in the [drafts section of your Iac Catalog](https://app.autocloud.io/iac-catalog/drafts):

![New IaC Catalog Blueprint](https://static1.autocloud.io/iac/getting-started/aws/getting-started-aws-card.png)

### Generate Code from Blueprint in AutoCloud

The Terraform blueprint is now deployed to AutoCloud. Next, test the blueprint to ensure proper functionality before publishing the blueprint to your organization.

#### Complete the Generation Form

In the [drafts section of your Iac Catalog](https://app.autocloud.io/iac-catalog/drafts), find the card labeled `[Getting Started] KMS Encrypted S3 Bucket`, and click the `Test` button. You will be brought to the code generation form wizard. Add a name for the bucket, and any tags you wish to associate with the resources:

![Complete the form](https://static1.autocloud.io/iac/getting-started/aws/getting-started-aws-form.png)

When you are done, click the `Next` button to continue to the review step.

#### Review the Submission

Review the submitted values, as these will be passed to the Terraform module. You can preview the Terraform code that will be generated with the `Review Code` button. You may return to the code generation wizard to make any corrections that you desire. Once you are satisfied, click the `Create` button to submit the configuration to AutoCloud to generate the code.


![Completed form](https://static1.autocloud.io/iac/getting-started/aws/getting-started-aws-complete.png)

#### Download the Generated Code

You have successfully completed the AutoCloud Terraform Blueprint code generation process. Click the `Download` button to download the generated code.


#### Run Terraform to Create S3 Bucket

In the terminal you configured access for, navigate to the downloaded code. Execute the Terraform to create the KMS encrypted S3 bucket:

```bash
% terraform init
% terraform plan
% terraform apply
```

Once complete, you will see the S3 bucket and the KMS key in your AWS account.

Your AutoCloud Terraform Blueprint is now ready to be deployed to the rest of your organization.

## Security

We deeply appreciate any effort to discover and disclose security vulnerabilities responsibly.

If you would like to report a vulnerability in one of our products, or have security concerns regarding AutoCloud software, please email security@autocloud.io.

In order for us to best respond to your report, please include any of the following:

Steps to reproduce or proof-of-concept
Any relevant tools, including versions used
Tool output