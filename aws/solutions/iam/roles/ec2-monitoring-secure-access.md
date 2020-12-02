---
description: >-
  Describes the process for deploying an IAM role that provides least privilege
  to EC2 for monitoring with CloudWatch Logs and Access/Inventory via AWS
  Systems Manager Agent (SSM).
---

# EC2 Instance Monitoring & Secure Access

## Permissions

A certain level of permissions is required to be supplied in the IAM Role attached to the Instance in order to log advanced monitoring to AWS CloudWatch as well as access, management, and inventory with AWS SSM.

The following explains the process to provide permissions to your EC2 Instance\(s\)

### No existing IAM Role

If you do not have an IAM Role created to attach to your instance, you can create one by using the _**Deployment**_ process provided in this document.

{% hint style="info" %}
The permissions provided in the Role that is deployed from this document include permissions for enabling EC2 Instances to create CloudWatch Logs and Access via SSM. This does not affect pricing or security. These are base recommended permissions for EC2 Instances.
{% endhint %}

### Exiting IAM Role

If you do have an IAM Role created and/or attached to your EC2 Instance\(s\) already, you can meet this requirement by attaching the AWS Managed IAM Policy:

#### CloudWatch Server Permissions

The CloudWatch Server Policy is used to provide an EC2 Instance permissions to generate logs in CloudWatch.

> iam::aws:policy/CloudWatchAgentServerPolicy

#### CloudWatch Admin Permissions

The CloudWatch Admin Policy is used to both allow the generation of logs in CloudWatch as well as configured the CloudWatch agent and write the configuration to an SSM Parameter Store.

> iam::aws:policy/CloudWatchAgentAdminPolicy

#### SSM Permissions Only

The SSM Managed Instance Core policy is what is required for the instance to be managed by the AWS Systems Manager Service and be listed in the SSM Inventory.

> iam::aws:policy/AmazonSSMManagedInstanceCore

### Attaching an IAM Role to EC2

To follow the correct process for attaching/changing an EC2 Instance Role, please visit:

{% embed url="https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/iam-roles-for-amazon-ec2.html\#attach-iam-role" caption="Modify EC2 Instance Role" %}

## Networking

The AWS SSM service communicates via outbound access from your EC2 Instances over HTTPS. This requires that you have a security group attached to your EC2 instance the allows `port 443` egress to the public.

If you cannot allow outbound access to the public on port 443 via NATing to being deployed in a public subnet, you will need to have the SSM VPC Endpoint attached to your VPC.

This is an advanced configuration that is out of scope for this document. Instructions for that process are provided here:

{% page-ref page="../../systems-manager/ssm-endpoint.md" %}

## Deployment

To deploy the IAM Role required for SSM via AWS CloudFormation into your AWS account\(s\) you must follow these steps.

1. Be logged into the AWS Account
2. Be in the region you wish to deploy this stack. TactfulCloud recommends `US EAST (N. Virginia) us-east-1`
3. From the same browser session click the **Launch Stack** button below for the desired deployment
4. Acknowledge \(Check Box\) in the CloudFormation Review window that this stack will deploy IAM Resources
5. Click the **Create** Button

{% hint style="warning" %}
Recommended: Deploy only the Server Role unless manual log configuration per EC2 instances is required.
{% endhint %}

| Permissions | Launch Button |
| :--- | :--- |
| Server Role | [![Launch Stack](https://cdn.rawgit.org/global.tactfulcloud.com/icons/AWS/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home#/stacks/create/review?stackName=role-ec2-cw-ssm&templateURL=https://s3.amazonaws.com/aws-support.tactfulcloud.com/iam/role-ec2-cw-ssm.yml&param_RoleType=Server) |
| Admin Role | [![Launch Stack](https://cdn.rawgit.org/global.tactfulcloud.com/icons/AWS/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home#/stacks/create/review?stackName=role-ec2-cw-ssm&templateURL=https://s3.amazonaws.com/aws-support.tactfulcloud.com/iam/role-ec2-cw-ssm.yml&param_RoleType=Admin) |
| Both | [![Launch Stack](https://cdn.rawgit.org/global.tactfulcloud.com/icons/AWS/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home#/stacks/create/review?stackName=role-ec2-cw-ssm&templateURL=https://s3.amazonaws.com/aws-support.tactfulcloud.com/iam/role-ec2-cw-ssm.yml&param_RoleType=Both) |

![launch-cw-ssm-role](../../../../.gitbook/assets/cft-cw-ssm-role.gif)

Or you can download the template from [https://s3.amazonaws.com/aws-support.tactfulcloud.com/iam/role-ec2-cw-ssm.yml](https://s3.amazonaws.com/aws-support.tactfulcloud.com/iam/role-ec2-cw-ssm.yml) to deploy manually.

