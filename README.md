# AWS EKS MasterClass on new AutoMode

# Amazon EKS Auto Mode Workshop

[**Session introduction**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop#session-introduction)

In this workshop you will gain hands-on experience with Amazon EKS Auto Mode features that simplify the way you manage and operate your EKS clusters and deploy your applications.

[**What will you learn?**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop#what-will-you-learn)

By the end of this session, you will have a solid understanding of how Amazon EKS Auto Mode simplifies cluster deployment, explore how you can start working with it today, and gain a hands-on experience with its capabilities.

[**1. Enable EKS Auto Mode**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop#1.-enable-eks-auto-mode)

You will understand the new Amazon EKS Auto Mode API and choose your preferred way of enabling it, whether it's using the AWS CLI, Terraform, the EKS CLI - eksctl, or the AWS console. You will deploy a sample application, using the [Retail Store](https://github.com/aws-containers/retail-store-sample-app)  application and see how Amazon EKS Auto Mode automatically provision the right compute for your workload, exposes it to traffic and manages its storage.

[**2. Work with EKS Auto Mode capabilities**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop#2.-work-with-eks-auto-mode-capabilities)

You will also gradually modify different component of the Retail Store application you've already deployed, to dive into the different possible configurations of compute, networking and storage capabilities of Amazon EKS Auto Mode.

[**3. Upgrade your cluster**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop#3.-upgrade-your-cluster)

You will understand how EKS cluster upgrades works with Amazon EKS Auto Mode and upgrade the cluster by yourself.

[**4. Migrate an existing workload**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop#4.-migrate-an-existing-workload)

You will experience handling migration of an applications already deployed in an EKS cluster to EKS Auto Mode.

# Option 1 - Start at an AWS Event

## **Running the workshop at an AWS Event**

To complete this workshop, you are provided with an AWS account via Workshop Studio. This AWS account has pre-provisioned infrastructure and IAM policies needed to complete this workshop. The goal of this section is to help you access this AWS account.

**Note:** This can be only available when provided by AWS during events or invited in email for virtual events.

# Option 2 - In your own AWS account

**AWS Guided Events**

If you'd rather attend an AWS guided workshop, please register [here](https://aws-experience.com/emea/smb/events/series/get-hands-on-with-amazon-eks)  for a session on a date and time that works for you.

## **Prerequisites**

This workshop is compatible with any AWS Region where Amazon EKS is available. The default region used will be the one configured on the machine/laptop you're running the installation from.

1. Access to an AWS account.
2. CloudFormation access to deploy the stack with the necessary IAM permissions to create and manage the following resources: IAM, VPC, Lambda, CodeBuild, EKS, EC2, and CloudFront.
3. Enable Service Linked role for ElasticLoadBalancing and EC2Spot
    - **AWS CLI**
    
    `aws iam create-service-linked-role --aws-service-name elasticloadbalancing.amazonaws.com  
    aws iam create-service-linked-role --aws-service-name spot.amazonaws.com`
    

**Note**

If the Service Linked Roles (SLRs) already exists, you will receive the following error which can be ignored.

`An error occurred (InvalidInput) when calling the CreateServiceLinkedRole operation: Service role name AWSServiceRoleForElasticLoadBalancing has been taken in this account, please try a different suffix.

An error occurred (InvalidInput) when calling the CreateServiceLinkedRole operation: Service role name AWSServiceRoleForEC2Spot has been taken in this account, please try a different suffix`

- **CloudShell**
1. [**1. To open CloudShell, Navigate to the AWS Console and Search for "CloudShell"](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/00-introduction/20-on-your-own-account#1.-to-open-cloudshell-navigate-to-the-aws-console-and-search-for-%22cloudshell%22)[2. Paste the following commands into CloudShell to enable the required Service Linked Roles.](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/00-introduction/20-on-your-own-account#2.-paste-the-following-commands-into-cloudshell-to-enable-the-required-service-linked-roles.)**
    - **CloudShell**
    
    ![](https://static.us-east-1.prod.workshops.aws/7c3be994-d644-4401-a817-8cd56d557506/static/images/introduction/self-hosted_slr-cloudshell.png?Key-Pair-Id=K36Q2WVO3JP7QD&Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9zdGF0aWMudXMtZWFzdC0xLnByb2Qud29ya3Nob3BzLmF3cy83YzNiZTk5NC1kNjQ0LTQ0MDEtYTgxNy04Y2Q1NmQ1NTc1MDYvKiIsIkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTc0OTA3NDM0NH19fV19&Signature=W6WTuafMUQvUflH%7EEhZzuRyjNJftCEdrCF0ejl38MozYLykI2mAetYKbF86h0RLLnGofroTZPhK4yllzqxsaaDSSyRgze9Fvpjk0Ms1L8UBqAyv4jFwndJaf%7E4fBxBzS2cHu3Rk0lLG4Xo5Cb8A9PVDycYG8E%7Ez0HoIo2kyXPShI1JRocSpKKGDl50WVnd%7EQ8pQrxUD3L-ENWiyWP3JiuvViPXvc8mUUlCiCY0u9Jk%7E0LFiQm68sCn44JqL07uXLX3MpmBTchq-uqZdXWv1w5pouYAg-w9wgD5az4UBmySpxyRIPWFycxq4Gdy08r-AkurESWkXfjl3Bh%7EDkAPvLDg__)
    
    `aws iam create-service-linked-role --aws-service-name elasticloadbalancing.amazonaws.com   
    aws iam create-service-linked-role --aws-service-name spot.amazonaws.com`
    
    ![](https://static.us-east-1.prod.workshops.aws/7c3be994-d644-4401-a817-8cd56d557506/static/images/introduction/self-hosted_slr-cloudshellpaste.png?Key-Pair-Id=K36Q2WVO3JP7QD&Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9zdGF0aWMudXMtZWFzdC0xLnByb2Qud29ya3Nob3BzLmF3cy83YzNiZTk5NC1kNjQ0LTQ0MDEtYTgxNy04Y2Q1NmQ1NTc1MDYvKiIsIkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTc0OTA3NDM0NH19fV19&Signature=W6WTuafMUQvUflH%7EEhZzuRyjNJftCEdrCF0ejl38MozYLykI2mAetYKbF86h0RLLnGofroTZPhK4yllzqxsaaDSSyRgze9Fvpjk0Ms1L8UBqAyv4jFwndJaf%7E4fBxBzS2cHu3Rk0lLG4Xo5Cb8A9PVDycYG8E%7Ez0HoIo2kyXPShI1JRocSpKKGDl50WVnd%7EQ8pQrxUD3L-ENWiyWP3JiuvViPXvc8mUUlCiCY0u9Jk%7E0LFiQm68sCn44JqL07uXLX3MpmBTchq-uqZdXWv1w5pouYAg-w9wgD5az4UBmySpxyRIPWFycxq4Gdy08r-AkurESWkXfjl3Bh%7EDkAPvLDg__)
    

## **Cost**

**Cleanup**

Remember to [Cleanup](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/200-cleanup) the resources after completing the workshop.

Provisioning this workshop environment in your AWS account will create resources that incur costs. The CloudFormation stack deploys multiple resources

| Used by | Module | Resource Type | Resource | Qty |
| --- | --- | --- | --- | --- |
| VS Code IDE | Getting Started | EC2 | t3.medium | 1 |
| VS Code IDE | Getting Started | EBS | 30GB GP3 | 1 |
| VS Code IDE | Getting Started | CloudFront | Distribution | 1 |
| Demo Cluster | Module 1,2,3 | VPC | NAT Gateway | 1 |
| Demo Cluster | Module 1, 2, 3 | EKS | Cluster | 1 |
| Migration Cluster | Module 4 | VPC | NAT Gateway | 1 |
| Migration Cluster | Module 4 | EKS | Cluster | 1 |
| Migration Cluster | Module 4 | EKS - Managed Node Group - system | m6g.large | 3 |
| Migration Cluster | Module 4 | EKS - Managed Node Group - apps | m5.large | 3 |
| Migration Cluster | Module 4 | EKS - Self-Managed Karpenter - apps | c6g.large | 2 |
| Migration Cluster | Module 4 | EKS - Fargate | 0.25vCPU, 0.5GB | 3 |
| Migration Cluster | Module 4 | EKS - EC2 | Application Load Balancer | 1 |

**Additional Cost**

Throughout the workshop, you will create additional resources beyond those listed above. While the exact costs may vary depending on your specific actions and usage, these additional resources typically include **EC2**, **EBS**, **KMS Key**, and multiple **ELBs** (ALB + NLB). Please be aware that these extra resources will contribute to the overall cost of running the workshop.

An average cost for running the workshop is estimated at **$6/hour** in the **us-east-1** region.

## **Bootstrapping the environment**

Use the AWS CloudFormation quick-create links below to launch the desired template in the appropriate AWS region. The CloudFormation output will provide the IDE URL and password to use for the workshop.

[**us-east-1 Launch**](https://us-east-1.console.aws.amazon.com/cloudformation/home#/stacks/quickcreate?templateUrl=https://ws-assets-prod-iad-r-iad-ed304a55c2ca1aee.s3.us-east-1.amazonaws.com/aadbd25d-43fa-4ac3-ae88-32d729af8ed4/eks-automode-workshop-self.json&stackName=eks-automode-workshop) [**us-east-2 Launch**](https://us-east-2.console.aws.amazon.com/cloudformation/home#/stacks/quickcreate?templateUrl=https://ws-assets-prod-iad-r-cmh-8d6e9c21a4dec77d.s3.us-east-2.amazonaws.com/aadbd25d-43fa-4ac3-ae88-32d729af8ed4/eks-automode-workshop-self.json&stackName=eks-automode-workshop) [**us-west-2 Launch**](https://us-west-2.console.aws.amazon.com/cloudformation/home#/stacks/quickcreate?templateUrl=https://ws-assets-prod-iad-r-pdx-f3b3f9f1a7d6a3d0.s3.us-west-2.amazonaws.com/aadbd25d-43fa-4ac3-ae88-32d729af8ed4/eks-automode-workshop-self.json&stackName=eks-automode-workshop) [**eu-west-1 Launch**](https://eu-west-1.console.aws.amazon.com/cloudformation/home#/stacks/quickcreate?templateUrl=https://ws-assets-prod-iad-r-dub-85e3be25bd827406.s3.eu-west-1.amazonaws.com/aadbd25d-43fa-4ac3-ae88-32d729af8ed4/eks-automode-workshop-self.json&stackName=eks-automode-workshop) [**eu-west-3 Launch**](https://eu-west-3.console.aws.amazon.com/cloudformation/home#/stacks/quickcreate?templateUrl=https://ws-assets-prod-iad-r-cdg-9e76383c31ad6229.s3.eu-west-3.amazonaws.com/aadbd25d-43fa-4ac3-ae88-32d729af8ed4/eks-automode-workshop-self.json&stackName=eks-automode-workshop) [**eu-north-1 Launch**](https://eu-north-1.console.aws.amazon.com/cloudformation/home#/stacks/quickcreate?templateUrl=https://ws-assets-prod-iad-r-arn-580aeca3990cef5a.s3.eu-north-1.amazonaws.com/aadbd25d-43fa-4ac3-ae88-32d729af8ed4/eks-automode-workshop-self.json&stackName=eks-automode-workshop) [**ap-southeast-1 Launch**](https://ap-southeast-1.console.aws.amazon.com/cloudformation/home#/stacks/quickcreate?templateUrl=https://ws-assets-prod-iad-r-sin-694a125e41645312.s3.ap-southeast-1.amazonaws.com/aadbd25d-43fa-4ac3-ae88-32d729af8ed4/eks-automode-workshop-self.json&stackName=eks-automode-workshop)

If you want to deploy in another region, you can download the CloudFormation template and run it in the region of your choice.

[**CloudFormation Template**](https://static.us-east-1.prod.workshops.aws/7c3be994-d644-4401-a817-8cd56d557506/assets/eks-automode-workshop-self.json?Key-Pair-Id=K36Q2WVO3JP7QD&Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9zdGF0aWMudXMtZWFzdC0xLnByb2Qud29ya3Nob3BzLmF3cy83YzNiZTk5NC1kNjQ0LTQ0MDEtYTgxNy04Y2Q1NmQ1NTc1MDYvKiIsIkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTc0OTA3NDM0NH19fV19&Signature=W6WTuafMUQvUflH~EhZzuRyjNJftCEdrCF0ejl38MozYLykI2mAetYKbF86h0RLLnGofroTZPhK4yllzqxsaaDSSyRgze9Fvpjk0Ms1L8UBqAyv4jFwndJaf~4fBxBzS2cHu3Rk0lLG4Xo5Cb8A9PVDycYG8E~z0HoIo2kyXPShI1JRocSpKKGDl50WVnd~Q8pQrxUD3L-ENWiyWP3JiuvViPXvc8mUUlCiCY0u9Jk~0LFiQm68sCn44JqL07uXLX3MpmBTchq-uqZdXWv1w5pouYAg-w9wgD5az4UBmySpxyRIPWFycxq4Gdy08r-AkurESWkXfjl3Bh~DkAPvLDg__)

**Service Quotas**

The CloudFormation stack deploys 3 VPCs and 2 EKS clusters. Since AWS imposes a default limit of 5 VPCs per region and 5 EIPs per region, request a quota increase as needed through [Service Quotas](https://console.aws.amazon.com/servicequotas/home/dashboard)  before deployment to prevent stack creation failures.

To increase number of VPCs per Region [VPCs per Region](https://console.aws.amazon.com/servicequotas/home/services/vpc/quotas/L-F678F1CE) , you will need to have available 3 VPCs

To increase number of Elastic IP addresses (EIPs) per Region [EC2-VPC Elastic IPs](https://console.aws.amazon.com/servicequotas/home/services/ec2/quotas/L-0263D0A3) , you will need to available 2 EIPs

**Enter a valid IAM role ARN that will be used to access EKS clusters (this is typically the IAM role you assume to work in your account).**

![](https://static.us-east-1.prod.workshops.aws/7c3be994-d644-4401-a817-8cd56d557506/static/images/introduction/self-hosted_quickstart.png?Key-Pair-Id=K36Q2WVO3JP7QD&Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9zdGF0aWMudXMtZWFzdC0xLnByb2Qud29ya3Nob3BzLmF3cy83YzNiZTk5NC1kNjQ0LTQ0MDEtYTgxNy04Y2Q1NmQ1NTc1MDYvKiIsIkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTc0OTA3NDM0NH19fV19&Signature=W6WTuafMUQvUflH%7EEhZzuRyjNJftCEdrCF0ejl38MozYLykI2mAetYKbF86h0RLLnGofroTZPhK4yllzqxsaaDSSyRgze9Fvpjk0Ms1L8UBqAyv4jFwndJaf%7E4fBxBzS2cHu3Rk0lLG4Xo5Cb8A9PVDycYG8E%7Ez0HoIo2kyXPShI1JRocSpKKGDl50WVnd%7EQ8pQrxUD3L-ENWiyWP3JiuvViPXvc8mUUlCiCY0u9Jk%7E0LFiQm68sCn44JqL07uXLX3MpmBTchq-uqZdXWv1w5pouYAg-w9wgD5az4UBmySpxyRIPWFycxq4Gdy08r-AkurESWkXfjl3Bh%7EDkAPvLDg__)

**Note**

This process might take a while (approximately 45 minutes).

Once the Stack creation Status is `CREATE_COMPLETE`, the creation of the workshop stack is done and you can proceed to the next step.

![](https://static.us-east-1.prod.workshops.aws/7c3be994-d644-4401-a817-8cd56d557506/static/images/introduction/self-hosted_stack.png?Key-Pair-Id=K36Q2WVO3JP7QD&Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9zdGF0aWMudXMtZWFzdC0xLnByb2Qud29ya3Nob3BzLmF3cy83YzNiZTk5NC1kNjQ0LTQ0MDEtYTgxNy04Y2Q1NmQ1NTc1MDYvKiIsIkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTc0OTA3NDM0NH19fV19&Signature=W6WTuafMUQvUflH%7EEhZzuRyjNJftCEdrCF0ejl38MozYLykI2mAetYKbF86h0RLLnGofroTZPhK4yllzqxsaaDSSyRgze9Fvpjk0Ms1L8UBqAyv4jFwndJaf%7E4fBxBzS2cHu3Rk0lLG4Xo5Cb8A9PVDycYG8E%7Ez0HoIo2kyXPShI1JRocSpKKGDl50WVnd%7EQ8pQrxUD3L-ENWiyWP3JiuvViPXvc8mUUlCiCY0u9Jk%7E0LFiQm68sCn44JqL07uXLX3MpmBTchq-uqZdXWv1w5pouYAg-w9wgD5az4UBmySpxyRIPWFycxq4Gdy08r-AkurESWkXfjl3Bh%7EDkAPvLDg__)

**Note**

The `eks-automode-workshop` stack will create a total of 11 stacks, this is an expected outcome. When you come to delete resources at the end of the workshop, deleting `eks-automode-workshop` will remove all associated stacks automatically.
# Access the cluster

In this workshop you will gain access to two pre-provisioned clusters.

The first cluster will be used to demonstrate and use EKS Auto Mode capabilities, while the second one will be used for the migration guidance module further in the workshop.

The cluster names are defined as two environment variables in the IDE:

1. `DEMO_CLUSTER_NAME`
2. `MIGRATION_CLUSTER_NAME`

We've also set up the access for both of those clusters, as well as installed tools to help you switch between `kubectl` contexts and Kubernetes namespaces like `kubectx` and `kubens`.

You can open a terminal with the Ctrl+Shift+~ shortcut. Alternatively, you can click **Toggle Panel** icon placed at the top right or the "hamburger" menu placed at the top left and select **Terminal**.

➤ First, set your current Kubernetes context to use the `demo-cluster` by running the following command in a VS Code terminal in your workshop lab environment:

`kubectx arn:aws:eks:${AWS_REGION}:${AWS_ACCOUNT_ID}:cluster/demo-cluster`

The result should be similar to the following output:

`Switched to context "arn:aws:eks:us-west-2:123456789:cluster/demo-cluster".`

Let's make sure that we have access to the demo cluster by listing the CRDs (Custom Resource Definitions) in the cluster.

➤ Execute, in your VS Code terminal:

`kubectl get crds`

You should see all the CRDs installed in the **demo** cluster:

`NAME                                         CREATED AT
cninodes.vpcresources.k8s.aws                2024-12-01T00:00:00Z
policyendpoints.networking.k8s.aws           2024-12-01T00:00:00Z
securitygrouppolicies.vpcresources.k8s.aws   2024-12-01T00:00:00Z`

Try to see if there're pods or nodes connected to the cluster. Did you find any?

➤ Running the following commands won't show any pods or nodes in the cluster. You should expect an output of `No resources found` for both commands:

`kubectl get pods --all-namespaces
kubectl get nodes`

The reason for that is that we are going to enable EKS Auto Mode in our cluster, which will provide us with capabilities such as compute, networking, storage, and security. You will find more about this later in this session.

With the cluster accessible, we can continue to the first module.

# Module 1 - Enable Amazon EKS Auto Mode and deploy a sample Application

This module will guide you through enabling Amazon EKS Auto Mode for existing cluster and deploying a sample application to explore its capabilities.

# Enable Amazon EKS Auto Mode

[Overview](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/10-enable-eks-auto-mode/10-enable-auto-mode#overview) | [Enable EKS Auto Mode](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/10-enable-eks-auto-mode/10-enable-auto-mode#enable-eks-auto-mode) | [Verify EKS Auto Mode](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/10-enable-eks-auto-mode/10-enable-auto-mode#verify) | [Summary](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/10-enable-eks-auto-mode/10-enable-auto-mode#summary)

---

## **Overview**

This module describes how to enable Amazon EKS Auto Mode on your existing Amazon EKS clusters. You will work with the pre-configured `demo-cluster`, which currently has no workloads or add-ons deployed. Using available API options, you will enable Auto Mode to understand the different ways to enable it. Finally, you will deploy a sample application to demonstrate EKS Auto Mode's simplified operations and automated infrastructure management.

**Note**

Enabling EKS Auto Mode on a cluster can take around 4 minutes

➤ Before starting, ensure you're using the context of the `demo-cluster` if you haven't done so in the [Getting started](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/00-introduction/20-cluster-access.md) section:

`kubectx arn:aws:eks:${AWS_REGION}:${AWS_ACCOUNT_ID}:cluster/demo-cluster`

The output should be similar to:

`Switched to context "arn:aws:eks:us-west-2:123456789:cluster/demo-cluster".`

## **Enable EKS Auto Mode**

This section describes how to enable Amazon EKS Auto Mode on your existing cluster using the eksctl util. Choose your preferred method to enable Amazon EKS Auto Mode for the provided cluster and explore how the updated API calls looks like for EKS Auto Mode.

- **AWS CLI**

This section describes how to enable Amazon EKS Auto Mode on your existing Amazon EKS clusters using AWS CLI.

[**1. Update the cluster IAM Role**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/10-enable-eks-auto-mode/10-enable-auto-mode#1.-update-the-cluster-iam-role)

[EKS Auto Mode docs](https://docs.aws.amazon.com/eks/latest/userguide/auto-cluster-iam-role.html)  describe IAM policies to be added to the cluster role, in addition to the already existing `AmazonEKSClusterPolicy`:

- [AmazonEKSComputePolicy](https://docs.aws.amazon.com/eks/latest/userguide/security-iam-awsmanpol.html#security-iam-awsmanpol-AmazonEKSComputePolicy)
- [AmazonEKSBlockStoragePolicy](https://docs.aws.amazon.com/eks/latest/userguide/security-iam-awsmanpol.html#security-iam-awsmanpol-AmazonEKSBlockStoragePolicy)
- [AmazonEKSNetworkingPolicy](https://docs.aws.amazon.com/eks/latest/userguide/security-iam-awsmanpol.html#security-iam-awsmanpol-AmazonEKSNetworkingPolicy)
- [AmazonEKSLoadBalancingPolicy](https://docs.aws.amazon.com/eks/latest/userguide/security-iam-awsmanpol.html#security-iam-awsmanpol-AmazonEKSLoadBalancingPolicy)

➤ You can either add these policies manually, through the AWS IAM console, or use the following command:

`for POLICY in \
  "arn:aws:iam::aws:policy/AmazonEKSComputePolicy" \
  "arn:aws:iam::aws:policy/AmazonEKSBlockStoragePolicy" \
  "arn:aws:iam::aws:policy/AmazonEKSLoadBalancingPolicy" \
  "arn:aws:iam::aws:policy/AmazonEKSNetworkingPolicy" \
  "arn:aws:iam::aws:policy/AmazonEKSClusterPolicy"
do
  echo "Attaching policy ${POLICY} to IAM role ${DEMO_CLUSTER_ROLE_NAME}..."
  aws iam attach-role-policy --role-name ${DEMO_CLUSTER_ROLE_NAME} --policy-arn ${POLICY}
done`

In addition, the trust policy of the cluster role need to be changed to allow EKS to automate routine tasks.

➤ Execute the following command to add the `tagSession` to the trust policy:

`aws iam update-assume-role-policy --role-name $DEMO_CLUSTER_ROLE_NAME --policy-document '{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "eks.amazonaws.com"
      },
      "Action": [
        "sts:AssumeRole",
        "sts:TagSession"
      ]
    }
  ]
}'`

➤ Verify that the IAM role has been updated properly:

`aws iam get-role --role-name ${DEMO_CLUSTER_ROLE_NAME} | \
  jq -r '.Role.AssumeRolePolicyDocument.Statement[].Action[]'

aws iam list-attached-role-policies --role-name ${DEMO_CLUSTER_ROLE_NAME} | \
  jq -r '.AttachedPolicies[].PolicyName'`

The output should be (note the `AmazonEKSClusterPolicy` that the role already had attached before):

`sts:AssumeRole
sts:TagSession
AmazonEKSClusterPolicy
AmazonEKSNetworkingPolicy
AmazonEKSComputePolicy
AmazonEKSBlockStoragePolicy
AmazonEKSLoadBalancingPolicy`

[**2. Enable EKS Auto Mode**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/10-enable-eks-auto-mode/10-enable-auto-mode#2.-enable-eks-auto-mode)

➤ You can now run the following command to enable EKS Auto Mode:

`aws eks update-cluster-config \
    --name ${DEMO_CLUSTER_NAME} \
    --compute-config enabled=true,nodeRoleArn=${DEMO_CLUSTER_NODE_ROLE_ARN},nodePools=system,general-purpose \
    --kubernetes-network-config '{"elasticLoadBalancing":{"enabled": true}}' \
    --storage-config '{"blockStorage":{"enabled": true}}'`

**Note**

The compute, block storage, and load balancing capabilities in the command above must all be enabled or disabled in the same request.

In addition to enabling these capabilities, we've also configured the node IAM role to be attached to EKS Auto Mode managed instances, and defined the two [built-in](https://docs.aws.amazon.com/eks/latest/userguide/set-builtin-node-pools.html)  EKS Auto Mode node pools. The `system` node pool is intended for cluster-critical applications, and the `general-purpose` node pool is intended for general purpose workloads in the cluster.

It might take couple of seconds for the cluster to get the API call from the CLI and reached to an "Updating" state. If any of the below commands shows that the cluster is "Active", please wait couple of seconds, and run it again.

➤ You can now check the upgrade status of the cluster using the following command:

`aws eks describe-cluster --name ${DEMO_CLUSTER_NAME} --query 'cluster.status'`

➤ Alternatively, you can run the following command to wait for the cluster to be in the `Active` state:

`aws eks wait cluster-active --name ${DEMO_CLUSTER_NAME}`

- **eksctl**

`eksctl` has added a new `autoModeConfig` field to make it easy to enable and configure Auto Mode. The shape of the autoModeConfig field is:

`autoModeConfig: # defaults to false
  enabled: boolean # optional, defaults to [general-purpose, system]. # To disable creation of nodePools, set it to the empty array ([]).
  nodePools: []string # optional, eksctl creates a new role if this is not supplied # and nodePools are present.
  nodeRoleARN: string`

If `autoModeConfig.enabled` is `true`, `eksctl` will:

1. Update your EKS cluster by passing the following to the EKS API, enabling management of data plane components like compute, storage and networking:
    - `computeConfig.enabled: true`
    - `kubernetesNetworkConfig.elasticLoadBalancing.enabled: true`
    - `storageConfig.blockStorage.enabled: true`
2. Create a new node role to use for the nodes launched by EKS Auto Mode, unless you provide the existing cluster's node role ARN (`nodeRoleARN: ${DEMO_CLUSTER_NODE_ROLE_ARN}`)
3. Create the default node pools (`general-purpose` and `system` node pools). To disable creation of the default node pools and configure your own node pools that use a different set of subnets, set `nodePools: []`
4. Update the existing [cluster IAM role](https://docs.aws.amazon.com/eks/latest/userguide/cluster-iam-role.html)  with the required permissions for the Auto Mode to operate. However, since the cluster role in the workshop was not originally created by eksctl, you will need to attach the IAM policies required by Auto Mode to the cluster role.

[**1. Update the cluster IAM Role**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/10-enable-eks-auto-mode/10-enable-auto-mode#1.-update-the-cluster-iam-role)

[EKS Auto Mode docs](https://docs.aws.amazon.com/eks/latest/userguide/auto-cluster-iam-role.html)  describe IAM policies to be added to the cluster role, in addition to the already existing `AmazonEKSClusterPolicy`:

- [AmazonEKSComputePolicy](https://docs.aws.amazon.com/aws-managed-policy/latest/reference/AmazonEKSComputePolicy.html)
- [AmazonEKSBlockStoragePolicy](https://docs.aws.amazon.com/aws-managed-policy/latest/reference/AmazonEKSBlockStoragePolicy.html)
- [AmazonEKSNetworkingPolicy](https://docs.aws.amazon.com/aws-managed-policy/latest/reference/AmazonEKSNetworkingPolicy.html)
- [AmazonEKSLoadBalancingPolicy](https://docs.aws.amazon.com/aws-managed-policy/latest/reference/AmazonEKSLoadBalancingPolicy.html)

➤ You can either add these policies manually, through the AWS IAM console, or use the following command:

`for POLICY in \
  "arn:aws:iam::aws:policy/AmazonEKSComputePolicy" \
  "arn:aws:iam::aws:policy/AmazonEKSBlockStoragePolicy" \
  "arn:aws:iam::aws:policy/AmazonEKSLoadBalancingPolicy" \
  "arn:aws:iam::aws:policy/AmazonEKSNetworkingPolicy" \
  "arn:aws:iam::aws:policy/AmazonEKSClusterPolicy"
do
  echo "Attaching policy ${POLICY} to IAM role ${DEMO_CLUSTER_ROLE_NAME}..."
  aws iam attach-role-policy --role-name ${DEMO_CLUSTER_ROLE_NAME} --policy-arn ${POLICY}
done`

In addition, the trust policy of the cluster role need to be changed to allow EKS to automate routine tasks.

➤ Execute the following command to add the `tagSession` to the trust policy:

`aws iam update-assume-role-policy --role-name $DEMO_CLUSTER_ROLE_NAME --policy-document '{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "eks.amazonaws.com"
      },
      "Action": [
        "sts:AssumeRole",
        "sts:TagSession"
      ]
    }
  ]
}'`

➤ Verify that the IAM role has been updated properly:

`aws iam get-role --role-name ${DEMO_CLUSTER_ROLE_NAME} | \
  jq -r '.Role.AssumeRolePolicyDocument.Statement[].Action[]'

aws iam list-attached-role-policies --role-name ${DEMO_CLUSTER_ROLE_NAME} | \
  jq -r '.AttachedPolicies[].PolicyName'`

The output should be (note the `AmazonEKSClusterPolicy` that the role already had attached before):

`sts:AssumeRole
sts:TagSession
AmazonEKSClusterPolicy
AmazonEKSNetworkingPolicy
AmazonEKSComputePolicy
AmazonEKSBlockStoragePolicy
AmazonEKSLoadBalancingPolicy`

[**2. Enable EKS Auto Mode**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/10-enable-eks-auto-mode/10-enable-auto-mode#2.-enable-eks-auto-mode)

➤ You can now execute the following command to enable Auto Mode:

`cat << EOF | eksctl update auto-mode-config -f -
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig
metadata:
    name: ${DEMO_CLUSTER_NAME} # your cluster's name.
    region: ${AWS_REGION} # your cluster's region.
    version: "1.30" # your cluster's current kubernetes version.

autoModeConfig:
    enabled: true
    nodePools: ["general-purpose", "system"]
    #Optional, eksctl creates a new role if this is not supplied.
    nodeRoleARN: ${DEMO_CLUSTER_NODE_ROLE_ARN} # The existing cluster's node role.
EOF`

- **Terraform**

This section describes how to enable Amazon EKS Auto Mode on your existing Amazon EKS clusters using Terraform. We will use an already created cluster named `demo-cluster`. Before you begin, ensure you have authenticated to Terraform with administrator access to your Amazon EKS cluster and permissions to modify IAM roles.

[**1. Update the cluster IAM Role**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/10-enable-eks-auto-mode/10-enable-auto-mode#1.-update-the-cluster-iam-role)

[EKS Auto Mode docs](https://docs.aws.amazon.com/eks/latest/userguide/auto-cluster-iam-role.html)  describe IAM policies to be added to the cluster role, in addition to the already existing `AmazonEKSClusterPolicy`:

- [AmazonEKSComputePolicy](https://docs.aws.amazon.com/aws-managed-policy/latest/reference/AmazonEKSComputePolicy.html)
- [AmazonEKSBlockStoragePolicy](https://docs.aws.amazon.com/aws-managed-policy/latest/reference/AmazonEKSBlockStoragePolicy.html)
- [AmazonEKSNetworkingPolicy](https://docs.aws.amazon.com/aws-managed-policy/latest/reference/AmazonEKSNetworkingPolicy.html)
- [AmazonEKSLoadBalancingPolicy](https://docs.aws.amazon.com/aws-managed-policy/latest/reference/AmazonEKSLoadBalancingPolicy.html)

These policies will be attached using a pre-defined `aws_iam_role_policy_attachment` Terraform resource, which can be found at `enable/main.tf` file in your VS Code file explorer.

Enabling EKS Auto Mode with [Terraform](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/eks_cluster#eks-cluster-with-eks-auto-mode)  requires setting `compute_config.enabled`, `kubernetes_network_config.elastic_load_balancing.enabled`, and `storage_config.block_storage.enabled` to `true`, as well as `bootstrap_self_managed_addons` to `false`.

`resource "aws_eks_cluster" "example" {
  name = "example"

  access_config {
    authentication_mode = "API"
  }

  role_arn = aws_iam_role.cluster.arn
  version  = "1.31"

  bootstrap_self_managed_addons = false

  compute_config {
    enabled       = true
    node_pools    = ["system","general-purpose"]
    node_role_arn = aws_iam_role.node.arn
  }

  kubernetes_network_config {
    elastic_load_balancing {
      enabled = true
    }
  }

  storage_config {
    block_storage {
      enabled = true
    }
  }
}`

In the VS Code file explorer, you will find the Terraform `enable` folder with the code that imports `demo-cluster` as an `aws_eks_cluster` resource and defines the changes in the `main.tf` file. You will also find the `variables.tf` file that is pre-populated with the relevant environment variables.

➤ Execute the following command to populate the variables:

`export \
    TF_VAR_aws_region=${AWS_REGION} \
    TF_VAR_cluster_name=${DEMO_CLUSTER_NAME} \
    TF_VAR_cluster_role_arn=${DEMO_CLUSTER_ROLE_ARN} \
    TF_VAR_cluster_role_name=${DEMO_CLUSTER_ROLE_NAME} \
    TF_VAR_node_role_arn=${DEMO_CLUSTER_NODE_ROLE_ARN}`

➤ First, let´s initialize Terraform:

`cd ~/environment/enable/terraform
terraform init`

Since the cluster already been created for you, we'll have to modify the Cluster IAM role trust policy per [EKS Auto Mode documentations](https://docs.aws.amazon.com/eks/latest/userguide/auto-enable-existing.html) . That means that before planning and applying the resources, we should import the AWS IAM Role to the Terraform state. The code that does that in the `main.tf` file you have in the your IDE is highlighted below:

`<previous `main.tf` content>
...
resource "aws_iam_role" "cluster_role" {
  name = var.cluster_role_name

  assume_role_policy = jsonencode({
    Version = "2012-10-17"
    Statement = [
      {
        Effect = "Allow"
        Principal = {
          Service = "eks.amazonaws.com"
        }
        Action = [
          "sts:AssumeRole",
          "sts:TagSession"
        ]
      }
    ]
  })
}
...
<other `main.tf` content>`

In real-life scenarios, you won't have to run this `terraform import` command as you should already have the IAM role managed by Terraform. In this case, you'll simply have to modify your Terraform code to include the additional trust policy permission as described in the [EKS Auto Mode documentation](https://docs.aws.amazon.com/eks/latest/userguide/auto-enable-existing.html) .

➤ Execute the following command to import the cluster IAM role to the Terraform state:

`terraform import aws_iam_role.cluster_role $DEMO_CLUSTER_ROLE_NAME`

➤ Now, let's review the changes that will be made to the resources:

`terraform plan`

You should expect changes to the IAM role trust policy, as well as 4 new policy attachments to the cluster IAM role, and a change to the cluster config which enable EKS Auto Mode with 2 node-pools.

[**2. Enable EKS Auto Mode**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/10-enable-eks-auto-mode/10-enable-auto-mode#2.-enable-eks-auto-mode)

➤ Apply the changes to actually enable EKS Auto Mode:

`terraform apply --auto-approve`

Terraform will provide information about changes status and display an `Apply complete!` message once it's finished.

## **Verify EKS Auto Mode**

➤ Once EKS Auto Mode has been enabled, you can verify the cluster state is now `Active`:

`aws eks describe-cluster --name ${DEMO_CLUSTER_NAME} --query 'cluster.status'`

➤ You can also check that new CRDs are installed in the cluster by running the following command. Those CRDs are created and managed by EKS Auto Mode.

`kubectl get crd | grep eks.amazonaws.com`

with the expected output being similar to this (where we filtered to leave only the EKS Auto Mode-provided CRDs):

`cninodes.eks.amazonaws.com                   2025-01-22T12:25:06Z
ingressclassparams.eks.amazonaws.com         2025-01-22T12:25:02Z
nodeclasses.eks.amazonaws.com                2025-01-22T12:25:02Z
nodediagnostics.eks.amazonaws.com            2025-01-22T12:25:02Z
targetgroupbindings.eks.amazonaws.com        2025-01-22T12:25:02Z`

---

## **Summary**

In this section you learnt how to enable Amazon EKS Auto Mode on an existing cluster using `eksctl`, `AWS CLI` and `Terraform`.

You can now move onto the next section to deploy a sample application into our cluster.

# Deploy a sample application

[Overview](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/10-enable-eks-auto-mode/20-deploy-sample-application#overview) | [Review the cluster](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/10-enable-eks-auto-mode/20-deploy-sample-application#review) | [Deploy the sample application](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/10-enable-eks-auto-mode/20-deploy-sample-application#deploy-sample-app) | [Summary](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/10-enable-eks-auto-mode/20-deploy-sample-application#summary)

---

## **Overview**

This section will help you to understand the fundamentals of EKS Auto Mode, and explain how to deploy applications. The power of Auto Mode is that you don’t need to do any additional cluster configuration before you can launch your workloads.

EKS Auto Mode extends AWS management of Kubernetes components beyond the cluster itself, to allow AWS to set up and manage the infrastructure requires for smooth operations of your workloads. You can delegate key infrastructure decisions and leverage the expertise of AWS for day-to-day operations. EKS Auto Mode includes many Kubernetes capabilities as managed components for compute autoscaling, pod and service networking, application load balancing, cluster DNS, block storage, and GPU support.

[**Sample application**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/10-enable-eks-auto-mode/20-deploy-sample-application#sample-application)

To demonstrate the capabilities EKS Auto Mode provides us, we will use a sample web store application where customers can browse a catalog, add items to their cart, and complete an order through the checkout process. The application has several components, such as UI, catalog, orders, carts, and checkout services, along with a backend database that requires persistent block storage, modeled as Kubernetes Deployments and Statefulsets.

To learn more about the design of an application, refer to [retail-store-app](https://github.com/aws-containers/retail-store-sample-app) . We will use Kubernetes ingress to access UI applications outside of the cluster and will configure catalog applications to use Amazon EBS persistent storage. To demonstrate how Amazon EKS Auto Mode improves performance, provides scalability, and enhances availability, we will configure the UI application to support autoscaling, pod topology spread constraints,and pod disruption budgets (PDBs).

![](https://static.us-east-1.prod.workshops.aws/7c3be994-d644-4401-a817-8cd56d557506/static/images/module_2_fundamentals/retail-store-app.png?Key-Pair-Id=K36Q2WVO3JP7QD&Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9zdGF0aWMudXMtZWFzdC0xLnByb2Qud29ya3Nob3BzLmF3cy83YzNiZTk5NC1kNjQ0LTQ0MDEtYTgxNy04Y2Q1NmQ1NTc1MDYvKiIsIkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTc0OTA3NDM0NH19fV19&Signature=W6WTuafMUQvUflH%7EEhZzuRyjNJftCEdrCF0ejl38MozYLykI2mAetYKbF86h0RLLnGofroTZPhK4yllzqxsaaDSSyRgze9Fvpjk0Ms1L8UBqAyv4jFwndJaf%7E4fBxBzS2cHu3Rk0lLG4Xo5Cb8A9PVDycYG8E%7Ez0HoIo2kyXPShI1JRocSpKKGDl50WVnd%7EQ8pQrxUD3L-ENWiyWP3JiuvViPXvc8mUUlCiCY0u9Jk%7E0LFiQm68sCn44JqL07uXLX3MpmBTchq-uqZdXWv1w5pouYAg-w9wgD5az4UBmySpxyRIPWFycxq4Gdy08r-AkurESWkXfjl3Bh%7EDkAPvLDg__)

## **Review the cluster**

➤ Before deploying the application, check the cluster state again like you did in the [introduction](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/00-introduction/20-cluster-access) section.

`kubectl get pods --all-namespaces
kubectl get nodes`

The expected result for both of the commands above is:

`No resources found`

➤ Verify that we do have access to the demo cluster by listing the CRDs (Custom Resource Definitions) in the cluster:

`kubectl get crds`

This should produce an output similar to the following:

`NAME                                         CREATED AT
cninodes.eks.amazonaws.com                   2024-12-04T13:03:50Z
cninodes.vpcresources.k8s.aws                2024-12-04T13:00:46Z
ingressclassparams.eks.amazonaws.com         2024-12-04T13:03:49Z
nodeclaims.karpenter.sh                      2024-12-04T13:03:39Z
nodeclasses.eks.amazonaws.com                2024-12-04T13:03:39Z
nodediagnostics.eks.amazonaws.com            2024-12-04T13:03:39Z
nodepools.karpenter.sh                       2024-12-04T13:03:39Z
policyendpoints.networking.k8s.aws           2024-12-04T13:00:46Z
securitygrouppolicies.vpcresources.k8s.aws   2024-12-04T13:00:46Z
targetgroupbindings.eks.amazonaws.com        2024-12-04T13:03:49Z`

As you can see, the cluster doesn't have any nodes or pods running on it. However, you can see that it has more CRDs than it had [in the beginning of the workshop](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/00-introduction/20-cluster-access) when we tested the cluster connectivity. This is the first change that happened after enabling EKS Auto Mode.

Those CRDs enable several crucial capabilities of EKS Auto Mode:

- `nodepools` support provisioning compute
- `ingressclassparams` and `targetgroupbinding` allow exposing applications, and
- `nodediagnostics` provide diagnostics capabilities

To explore these capabilities, we will, initially, deploy the application in a manner that is self-contained in the Amazon EKS cluster, without using any AWS services that provision load balancers or managed databases. Over the course of the sections in this module we will leverage different features of Amazon EKS Auto Mode to take advantage of broader AWS services and features to enable our retail store operations and functionality.

[**Deploy the sample application**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/10-enable-eks-auto-mode/20-deploy-sample-application#deploy-sample-app)

We will use [Helm](https://helm.sh/)  charts for each of the components (catalog, order, UI etc.) to install the application. The code below contains a `helm install` command for each component and creates a `values-ui.yaml` file to specify UI application specific requirements and configure the components' endpoints.

[**Sample App Helm Values**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/10-enable-eks-auto-mode/20-deploy-sample-application#sample-app-helm-values)

Execute the following commands to deploy the sample application:

`cat << EOF > ~/environment/values-ui.yaml
endpoints:
    catalog: http://retail-store-app-catalog:80
    carts: http://retail-store-app-carts:80
    checkout: http://retail-store-app-checkout:80
    orders: http://retail-store-app-orders:80
    assets: http://retail-store-app-assets:80
EOF

helm upgrade -i retail-store-app-catalog oci://public.ecr.aws/aws-containers/retail-store-sample-catalog-chart --version ${RETAIL_STORE_APP_HELM_CHART_VERSION} --hide-notes
helm upgrade -i retail-store-app-orders oci://public.ecr.aws/aws-containers/retail-store-sample-orders-chart --version ${RETAIL_STORE_APP_HELM_CHART_VERSION} --hide-notes
helm upgrade -i retail-store-app-carts oci://public.ecr.aws/aws-containers/retail-store-sample-cart-chart --version ${RETAIL_STORE_APP_HELM_CHART_VERSION} --hide-notes
helm upgrade -i retail-store-app-checkout oci://public.ecr.aws/aws-containers/retail-store-sample-checkout-chart --version ${RETAIL_STORE_APP_HELM_CHART_VERSION} --hide-notes
helm upgrade -i retail-store-app-assets oci://public.ecr.aws/aws-containers/retail-store-sample-assets-chart --version ${RETAIL_STORE_APP_HELM_CHART_VERSION} --hide-notes
helm upgrade -i retail-store-app-ui oci://public.ecr.aws/aws-containers/retail-store-sample-ui-chart --version ${RETAIL_STORE_APP_HELM_CHART_VERSION} -f values-ui.yaml --hide-notes`

The commands above should produce helm outputs for each component of the app (`catalog`, `orders`, `cart`, `checkout`, `assets`, and `ui`) similar to the following output:

`[...]
NAME: retail-store-app-ui
LAST DEPLOYED: Mon Jan 20 17:42:52 2025
NAMESPACE: default
STATUS: deployed
REVISION: 1
[...]`

Amazon EKS Auto Mode will evaluate the resource requirements of these pods and determine the optimum compute to launch for your applications to run, considering any scheduling constraints configured.

➤ Wait for for the nodes to become `Ready` by executing, in a separate VS Code terminal:.

`kubectl wait --for=condition=Ready nodes --all`

After a couple of minutes, the nodes should be ready:

`node/i-0832abcbbc0911bee condition met`

Note that EC2 Instances created by EKS Auto Mode are different from other EC2 Instances, they are managed instances. These managed instances are owned by EKS and are more restricted. You can’t directly access or install software on instances managed by EKS Auto Mode.

➤ Open a separate terminal by clicking on the **+** icon on the top right of the IDE, and watch for application to become available:

`kubectl wait --for=condition=available deployments --all`

This is the expected result for an available application:

`deployment.apps/retail-store-app-assets condition met
deployment.apps/retail-store-app-carts condition met
deployment.apps/retail-store-app-carts-dynamodb condition met
deployment.apps/retail-store-app-catalog condition met
deployment.apps/retail-store-app-checkout condition met
deployment.apps/retail-store-app-checkout-redis condition met
deployment.apps/retail-store-app-orders condition met
deployment.apps/retail-store-app-ui condition met`

➤ Verify that all the components of the retail store applications are now running:

`kubectl get pods`

This should produce an output similar to this:

`NAME                                               READY   STATUS    RESTARTS      AGE
retail-store-app-assets-5d5d9d9dfc-8bwc2          1/1     Running   0               6m22s
retail-store-app-carts-5748d56f9b-8246m           1/1     Running   1 (4m33s ago)   6m22s
retail-store-app-carts-dynamodb-f6d4cd95b-n6p87   1/1     Running   0               6m22s
retail-store-app-catalog-667f4798c8-djvhc         1/1     Running   4 (4m22s ago)   6m21s
retail-store-app-catalog-mysql-0                  1/1     Running   0               6m21s
retail-store-app-checkout-5b74cbc869-csr7q        1/1     Running   0               6m22s
retail-store-app-checkout-redis-fbdd44cfc-znn9h   1/1     Running   0               6m22s
retail-store-app-orders-6c5cfd658f-tc8cn          1/1     Running   1 (4m37s ago)   6m21s
retail-store-app-orders-postgresql-0              1/1     Running   0               6m21s
retail-store-app-orders-rabbitmq-0                1/1     Running   0               6m21s
retail-store-app-ui-75cfd7c8fd-b2jp2              1/1     Running   0               6m22s`

Notice we have a pod for our catalog API and another for the corresponding MySQL database. If the catalog pod is showing a status of `CrashLoopBackOff`, it needs to be able to connect to the catalog's MySQL pod before it will start. Kubernetes will keep restarting it until this is the case.

We also created a Service for each of our application components, allowing communication between the components.

➤ Execute the following command:

`kubectl get svc`

`NAME                                 TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)              AGE
kubernetes                           ClusterIP   10.100.0.1       <none>        443/TCP              4h45m
retail-store-app-assets              ClusterIP   10.100.34.35     <none>        80/TCP               6m51s
retail-store-app-carts               ClusterIP   10.100.117.194   <none>        80/TCP               6m51s
retail-store-app-carts-dynamodb      ClusterIP   10.100.90.133    <none>        8000/TCP             6m51s
retail-store-app-catalog             ClusterIP   10.100.242.26    <none>        80/TCP               6m51s
retail-store-app-catalog-mysql       ClusterIP   10.100.128.150   <none>        3306/TCP             6m51s
retail-store-app-checkout            ClusterIP   10.100.125.1     <none>        80/TCP               6m51s
retail-store-app-checkout-redis      ClusterIP   10.100.147.192   <none>        6379/TCP             6m51s
retail-store-app-orders              ClusterIP   10.100.210.127   <none>        80/TCP               6m50s
retail-store-app-orders-postgresql   ClusterIP   10.100.141.36    <none>        5432/TCP             6m50s
retail-store-app-orders-rabbitmq     ClusterIP   10.100.249.147   <none>        5672/TCP,15672/TCP   6m50s
retail-store-app-ui                  ClusterIP   10.100.83.147    <none>        80/TCP               6m51s`

These Services are internal to the cluster, so we cannot access them from the Internet or even the VPC. However, we can use [port-forwarding](https://kubernetes.io/docs/tasks/access-application-cluster/port-forward-access-application-cluster/)  to access an existing Pod in the EKS cluster to check the application UI is working.

➤ Create a port-forwarding tunnel:

`kubectl port-forward $(kubectl get pods \
 --selector=app.kubernetes.io/name=ui -o jsonpath='{.items[0].metadata.name}') 8080:8080`

This should result in the following output:

`Forwarding from 127.0.0.1:8080 -> 8080
Forwarding from [::1]:8080 -> 8080
Handling connection for 8080
Handling connection for 8080`

You can now access the application using the localhost endpoint [http://localhost:8080/](http://localhost:8080/) . To do that, use the pop-up window that will appear on the bottom right side of the terminal. This will allow you to open the application in a new browser tab. The pop-up should looks like the below:

![](https://static.us-east-1.prod.workshops.aws/7c3be994-d644-4401-a817-8cd56d557506/static/images/10-enable-eks-auto-mode/port-forward-pop-up.png?Key-Pair-Id=K36Q2WVO3JP7QD&Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9zdGF0aWMudXMtZWFzdC0xLnByb2Qud29ya3Nob3BzLmF3cy83YzNiZTk5NC1kNjQ0LTQ0MDEtYTgxNy04Y2Q1NmQ1NTc1MDYvKiIsIkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTc0OTA3NDM0NH19fV19&Signature=W6WTuafMUQvUflH%7EEhZzuRyjNJftCEdrCF0ejl38MozYLykI2mAetYKbF86h0RLLnGofroTZPhK4yllzqxsaaDSSyRgze9Fvpjk0Ms1L8UBqAyv4jFwndJaf%7E4fBxBzS2cHu3Rk0lLG4Xo5Cb8A9PVDycYG8E%7Ez0HoIo2kyXPShI1JRocSpKKGDl50WVnd%7EQ8pQrxUD3L-ENWiyWP3JiuvViPXvc8mUUlCiCY0u9Jk%7E0LFiQm68sCn44JqL07uXLX3MpmBTchq-uqZdXWv1w5pouYAg-w9wgD5az4UBmySpxyRIPWFycxq4Gdy08r-AkurESWkXfjl3Bh%7EDkAPvLDg__)

The app might not render properly as it currently doesn't support proxy forwarding (which is how the vscode IDE server the `port-forward` command). You can ignore this as this has nothing to do with the cluster configuration, and the UI will be presented properly when you will expose the app via load balancer (ALB) in a later module.

---

[**Summary**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/10-enable-eks-auto-mode/20-deploy-sample-application#summary)

This section demonstrated deploying a multi-component retail store application, showcasing how EKS Auto Mode automatically evaluates resource requirements and provisions appropriate compute resources.

In the next section, we will focus on launching worker nodes in EKS Auto Mode and learning how to control Pod topology for our application.

# Module 2 - Explore EKS Auto Mode capabilities & fundamentals

This section will guide you through fundamentals of EKS Auto Mode and explain in details application components deployment using EKS Auto Mode.

# Compute

This section will cover the compute capabilities that are available with EKS Auto Mode, and provide a comprehensive understanding of how to optimize your compute resources for performance, availability, and cost.

# Node Launch

[Overview](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/20-nodelaunch#overview) | [Review the EKS Auto Mode configuration](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/20-nodelaunch#review-eks-auto-mode-config) | [Scale the application](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/20-nodelaunch#scale-app) | [Improve the application resilience](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/20-nodelaunch#improve-resilience) | [Summary](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/20-nodelaunch#summary)

---

## **Overview**

In EKS Auto Mode, your cluster’s compute resources are automatically provisioned and managed by EKS. Amazon EKS Auto Mode automates routine tasks for creating new EC2 Instances, and attaches them as nodes to your EKS cluster. EKS Auto Mode detects when a workload can’t be scheduled onto existing nodes, and creates a new, right-sized EC2 Instance.

EC2 Instances created by EKS Auto Mode are [EC2 managed instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/amazon-ec2-managed-instances.html) . Managed instances provide a simplified way for running compute workloads on Amazon EC2 by allowing you to delegate operational control of the instance to a service provider, in this case, EKS Auto Mode.

Because managed instances allow you to delegate control to the service provider, you can benefit from AWS’s operational expertise and best practices for running Amazon EKS. When an instance is managed, EKS is responsible for tasks such as provisioning the instance, configuring software, scaling capacity, and handling instance failures and replacements. You can still view the EKS Auto Mode managed instances in the AWS console and use instance storage as ephemeral storage for workloads. You can check the list of instance types supported by EKS Auto Mode [here](https://docs.aws.amazon.com/eks/latest/userguide/automode-learn-instances.html#auto-supported-instances)  and review the documentation for a [detailed comparison](https://docs.aws.amazon.com/eks/latest/userguide/automode-learn-instances.html#_comparison_table)  between standard EC2 instances and EKS Auto Mode managed instances.

Note that you can’t directly access or install software on instances managed by EKS Auto Mode.

## **Review the EKS Auto Mode configuration**

In EKS Auto Mode, node provisioning relies on [Karpenter](https://karpenter.sh/)  objects, with dedicated specification for EKS Auto Mode of [NodeClass](https://docs.aws.amazon.com/eks/latest/userguide/create-node-class.html)  and [NodePools](https://docs.aws.amazon.com/eks/latest/userguide/create-node-pool.html) .

The NodeClass specification defines infrastructure-level settings that apply to groups of nodes in your EKS cluster, including network configuration, storage settings, and resource tagging.

The NodePool specification allows for fine-grained control over your EKS cluster’s compute resources through various supported labels and requirements. These include options for specifying EC2 instance categories, CPU configurations, availability zones, architectures (ARM64/AMD64), and capacity types (spot/on-demand). You can also set resource limits for CPU and memory usage, ensuring your cluster stays within desired operational boundaries.

By default EKS Auto Mode includes two managed node pools: `general-purpose` and `system`. The `general-purpose` node pool is designed to handle user-deployed applications and services, whereas the `system` node pool is reserved for critical system-level components for managing the cluster's operation. As we will see later on, you can also create custom node pools if you have different compute or configuration requirements.

Let's explore the built-in node pools and their managed instances.

[**Review node pools configuration**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/20-nodelaunch#review-node-pools-configuration)

➤ View the managed instances that belong to the `general-purpose` node pool:

`kubectl get nodes -l karpenter.sh/nodepool=general-purpose`

The output should show a single managed instance:

`NAME                  STATUS   ROLES    AGE   VERSION
i-05e5427f9dc2f4b2e   Ready    <none>   31m   v1.31.3-eks-7636447`

➤ View the managed instances that belong to the `system` node pool:

`kubectl get nodes -l karpenter.sh/nodepool=system`

This should produce an empty result:

`No resources found`

Note: The `system` node pool is currently empty as no system components have been installed. All application pods are running on the `general-purpose` node pool.

➤ You can verify this by checking the pod distribution across the general-purpose nodes:

`for node in $(kubectl get nodes -l karpenter.sh/nodepool=general-purpose -o custom-columns=NAME:.metadata.name --no-headers); do
  echo "Pods on $node:"
  kubectl get pods --all-namespaces --field-selector spec.nodeName=$node
done`

The expected output should be similar to the following:

`Pods on i-05e5427f9dc2f4b2e:
NAMESPACE   NAME                                              READY   STATUS    RESTARTS      AGE
default     retail-store-app-assets-5d5d9d9dfc-f9g24          1/1     Running   0             32m
default     retail-store-app-carts-5748d56f9b-t6xh5           1/1     Running   0             32m
default     retail-store-app-carts-dynamodb-f6d4cd95b-8m4nz   1/1     Running   0             32m
default     retail-store-app-catalog-667f4798c8-x9lnn         1/1     Running   4 (30m ago)   32m
default     retail-store-app-catalog-mysql-0                  1/1     Running   0             32m
default     retail-store-app-checkout-5b74cbc869-rxbg9        1/1     Running   0             32m
default     retail-store-app-checkout-redis-fbdd44cfc-q27f4   1/1     Running   0             32m
default     retail-store-app-orders-6c5cfd658f-nxqxb          1/1     Running   1 (30m ago)   32m
default     retail-store-app-orders-postgresql-0              1/1     Running   0             32m
default     retail-store-app-orders-rabbitmq-0                1/1     Running   0             32m
default     retail-store-app-ui-75cfd7c8fd-gph9z              1/1     Running   0             32m`

Currently, all pods are running on a single node since it adequately meets the resource requirements of our workloads, that do not have any specific scheduling requirements.

## **Scale the application**

In this step, we will manually scale the application UI component replicas to see how Auto Mode automatically provisions new nodes to satisfy the growing demand.

➤ In a separate VS Code terminal, watch for new nodes by executing the command below:

`watch kubectl get nodes`

The above command will continuously watch and show changes to the cluster nodes. You can exit the command by pressing Ctrl/Cmd+C in its terminal.

➤ Scale the UI component:

`kubectl scale --replicas=12 deployment/retail-store-app-ui`

This should produce this output:

`deployment.apps/retail-store-app-ui scaled`

The watch command output should eventually show new nodes (with the `NotReady` status) being added to the cluster to accommodate the added UI component replicas:

`Every 2.0s: kubectl get nodes                                                                ip-192-168-0-253.us-west-2.compute.internal: Tue Feb 25 21:23:39 2025

NAME                  STATUS   ROLES    AGE   VERSION
i-00642042ad4eff3c9   Ready    <none>   17s   v1.30.8-eks-3c20087
i-009db40705eb0417d   Ready    <none>   10m   v1.30.8-eks-3c20087`

➤ Finally, if you're looking to see how EKS Auto Mode reacted to the installed app, you can look at the cluster events by running:

`kubectl events`

The output should include events registered against pods, NodePools, and Nodes.

**Expand to view the events**

➤ Now that our UI component has been scaled out, let's check the pod distribution:

`for node in $(kubectl get nodes -l karpenter.sh/nodepool=general-purpose -o custom-columns=NAME:.metadata.name --no-headers); do
  echo "Pods on $node:"
  kubectl get pods --all-namespaces --field-selector spec.nodeName=$node
done`

The command should produce an output similar to the following:

`Pods on i-05e5427f9dc2f4b2e:
NAMESPACE   NAME                                              READY   STATUS    RESTARTS      AGE
default     retail-store-app-assets-5d5d9d9dfc-f9g24          1/1     Running   0             36m
default     retail-store-app-carts-5748d56f9b-t6xh5           1/1     Running   0             36m
default     retail-store-app-carts-dynamodb-f6d4cd95b-8m4nz   1/1     Running   0             36m
default     retail-store-app-catalog-667f4798c8-x9lnn         1/1     Running   4 (34m ago)   36m
default     retail-store-app-catalog-mysql-0                  1/1     Running   0             36m
default     retail-store-app-checkout-5b74cbc869-rxbg9        1/1     Running   0             36m
default     retail-store-app-checkout-redis-fbdd44cfc-q27f4   1/1     Running   0             36m
default     retail-store-app-orders-6c5cfd658f-nxqxb          1/1     Running   1 (34m ago)   36m
default     retail-store-app-orders-postgresql-0              1/1     Running   0             36m
default     retail-store-app-orders-rabbitmq-0                1/1     Running   0             36m
default     retail-store-app-ui-75cfd7c8fd-5c9zv              1/1     Running   0             3m22s
default     retail-store-app-ui-75cfd7c8fd-gph9z              1/1     Running   0             36m
Pods on i-07b7c94f6bc1c5337:
NAMESPACE   NAME                                   READY   STATUS    RESTARTS      AGE
default     retail-store-app-ui-75cfd7c8fd-8tvzs   1/1     Running   1 (70s ago)   3m23s
default     retail-store-app-ui-75cfd7c8fd-b5tmw   1/1     Running   1 (65s ago)   3m23s
default     retail-store-app-ui-75cfd7c8fd-c8fbs   1/1     Running   1 (70s ago)   3m23s
default     retail-store-app-ui-75cfd7c8fd-fhxmc   1/1     Running   1 (64s ago)   3m23s
default     retail-store-app-ui-75cfd7c8fd-fxkn7   1/1     Running   1 (71s ago)   3m23s
default     retail-store-app-ui-75cfd7c8fd-msl6l   1/1     Running   1 (66s ago)   3m23s
default     retail-store-app-ui-75cfd7c8fd-p9srz   1/1     Running   1 (67s ago)   3m23s
default     retail-store-app-ui-75cfd7c8fd-qh4fj   1/1     Running   1 (71s ago)   3m23s
default     retail-store-app-ui-75cfd7c8fd-rk6xl   1/1     Running   1 (70s ago)   3m23s
default     retail-store-app-ui-75cfd7c8fd-twdvk   1/1     Running   1 (70s ago)   3m23s`

Note that the pods are currently densely packed and scheduled onto a single node, which reduces resilience. In the next step, we’ll explore how to improve that using EKS Auto Mode capabilities.

## **Improve the application resilience**

[**Topology spread constraints**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/20-nodelaunch#topology-spread-constraints)

To enhance the resilience of the application, it is critical to distribute pods across multiple AZs and nodes. Let’s apply [Pod Topology Spread Constraints](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/)  to our sample application UI component to ensure better fault tolerance and distribution.

We will update the UI component configuration accordingly and re-deploy it to apply the changes.

[**Update the UI component**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/20-nodelaunch#update-the-ui-component)

➤ Update the `values-ui.yaml` file and re-deploy the Helm chart:

`cat  << EOF >~/environment/values-ui.yaml
endpoints:
  catalog: http://retail-store-app-catalog:80
  carts: http://retail-store-app-carts:80
  checkout: http://retail-store-app-checkout:80
  orders: http://retail-store-app-orders:80
  assets: http://retail-store-app-assets:80

topologySpreadConstraints:
  - maxSkew: 1
    minDomains: 3
    topologyKey: topology.kubernetes.io/zone
    whenUnsatisfiable: DoNotSchedule
    labelSelector:
      matchLabels:
        app.kubernetes.io/name: ui
EOF

helm upgrade -f ~/environment/values-ui.yaml retail-store-app-ui oci://public.ecr.aws/aws-containers/retail-store-sample-ui-chart --version ${RETAIL_STORE_APP_HELM_CHART_VERSION} --hide-notes`

The output should be similar to:

`Pulled: public.ecr.aws/aws-containers/retail-store-sample-ui-chart:0.8.5
Digest: sha256:5cd721c10214c306b06c7223367f626f21a8d471eee8f0a576742426f84141f2
Release "retail-store-app-ui" has been upgraded. Happy Helming!
NAME: retail-store-app-ui
LAST DEPLOYED: Mon Jan 20 20:33:32 2025
NAMESPACE: default
STATUS: deployed
REVISION: 2`

The configuration specifies a maximum skew of 1 for both levels, meaning the difference in the number of pods between any two zones or any two nodes should not exceed 1. We've also set `minDomains` to be 3 (as the minimal number of AZs) to ensure proper distribution.

**Note**

The manually-scaled UI component will automatically reset to the default number of replicas (which is 1) after we deploy the updated configuration.

➤ Now, let's scale the application **again** to see how pod spread topology impacts the scaling behavior:

`kubectl scale --replicas=12 deployment/retail-store-app-ui`

As before, this is the expected output:

`deployment.apps/retail-store-app-ui scaled`

➤ Use the following command to wait for all the scaled UI component pods to become ready

`kubectl wait --for=condition=Ready pod -l app.kubernetes.io/instance=retail-store-app-ui --namespace default --timeout=300s`

➤ Now you can run the following command to see that the UI component pods spread across the different availability-zones.

`kubectl get node -L topology.kubernetes.io/zone --no-headers | while read node status roles age version zone; do
echo "Pods on node $node (Zone: $zone):"
  kubectl get pods --all-namespaces --field-selector spec.nodeName=$node -l app.kubernetes.io/instance=retail-store-app-ui
echo "-----------------------------------"
done`

This should produce an output similar to the following:

`Pods on node i-08e738621725e7f94 (Zone: us-west-2b):
NAMESPACE   NAME                                   READY   STATUS    RESTARTS   AGE
default     retail-store-app-ui-7bc7b7b49f-9smmr   1/1     Running   0          60s
default     retail-store-app-ui-7bc7b7b49f-blfg6   1/1     Running   0          60s
default     retail-store-app-ui-7bc7b7b49f-btwv9   1/1     Running   0          61s
default     retail-store-app-ui-7bc7b7b49f-jvzkx   1/1     Running   0          60s
-----------------------------------
Pods on node i-0ccba201de23807ec (Zone: us-west-2d):
NAMESPACE   NAME                                   READY   STATUS    RESTARTS   AGE
default     retail-store-app-ui-7bc7b7b49f-mnz7k   1/1     Running   0          16m
default     retail-store-app-ui-7bc7b7b49f-pvwrq   1/1     Running   0          61s
-----------------------------------
Pods on node i-0d595eff675936a84 (Zone: us-west-2d):
NAMESPACE   NAME                                   READY   STATUS    RESTARTS   AGE
default     retail-store-app-ui-7bc7b7b49f-28hbv   1/1     Running   0          63s
default     retail-store-app-ui-7bc7b7b49f-j4kzl   1/1     Running   0          63s
-----------------------------------
Pods on node i-0f66e5e0f8c881064 (Zone: us-west-2c):
NAMESPACE   NAME                                   READY   STATUS    RESTARTS   AGE
default     retail-store-app-ui-7bc7b7b49f-bptqk   1/1     Running   0          65s
default     retail-store-app-ui-7bc7b7b49f-m7wjp   1/1     Running   0          65s
default     retail-store-app-ui-7bc7b7b49f-nnjhs   1/1     Running   0          66s
default     retail-store-app-ui-7bc7b7b49f-zh9vt   1/1     Running   0          66s
-----------------------------------`

The pod topology spread constraints have successfully distributed the workload across multiple AZs and nodes, ensuring high availability and fault tolerance.

## **Summary**

In this section we've reviewed the EKS Auto Mode built-in `system` and `general-purpose` node pools, manually scaled the application and improved its resilience by apply AZ-level topology spread constraints to the UI component.

In the next section we will explore how to implement automated scaling policies for the UI application, replacing manual scaling operations. We will examine how EKS Auto Mode manages dynamic resource allocation and workload distribution in response to these policies.

# Autoscaling

[Overview](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/30-autoscaling#overview) | [Horizontal Pod Autoscaling](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/30-autoscaling#hpa) | [Summary](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/30-autoscaling#summary)

---

This section will guide you through the basics of EKS Auto Mode and explore, in details, application and cluster autoscaling.

## **Overview**

[**Disruptions in EKS Auto Mode**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/30-autoscaling#disruptions-in-eks-auto-mode)

Before we dive into autoscaling, let's first understand how [disruptions](https://docs.aws.amazon.com/eks/latest/userguide/create-node-pool.html#_disruption)  are managed in EKS Auto Mode. Disruptions can occur in situations such as when nodes are scaled down to reduce cluster costs (like bin-packing), or hit their maximum lifetime (expiry date). This potentially impacts the running pods on those nodes. EKS Auto Mode uses Karpenter under the hood to optimize node scaling and manage these disruptions effectively.

Karpenter manages node disruptions through three key mechanisms: expiration, drift detection, and consolidation, with the latter being the focus of this section, as more relevant to autoscaling.

[**Consolidation**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/30-autoscaling#consolidation)

Consolidation works by continuously monitoring the utilization of nodes and pods in the cluster. When nodes become underutilized or idle, Karpenter initiates a consolidation process to optimize cluster resources. This involves removing nodes without active workloads, efficiently bin-packing pods onto existing nodes where capacity permits, and performing graceful node draining by carefully evicting and rescheduling pods to maintain application availability throughout the consolidation process.

Below you can see the highlighted configuration of the `disruption` block in the provided `general-purpose` NodePool that is created and managed by EKS Auto Mode

➤ Get the NodePool configuration:

`kubectl get nodepools general-purpose -o yaml`

This should show the following output:

`apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
  annotations:
    karpenter.sh/nodepool-hash: "4012513481623584108"
    karpenter.sh/nodepool-hash-version: v3
  creationTimestamp: "2025-01-15T09:32:29Z"
  generation: 1
  labels:
    app.kubernetes.io/managed-by: eks
  name: general-purpose
  resourceVersion: "241001"
  uid: 9b1c4ad0-d42d-4c63-bd96-b0a201aeec0e
spec:
  disruption:
    budgets:
    - nodes: 10%
    consolidateAfter: 30s
    consolidationPolicy: WhenEmptyOrUnderutilized
  template:
    metadata: {}
    spec:
      expireAfter: 336h
      nodeClassRef:
        group: eks.amazonaws.com
        kind: NodeClass
        name: default
      requirements:
      - key: karpenter.sh/capacity-type
        operator: In
        values:
        - on-demand
      - key: eks.amazonaws.com/instance-category
        operator: In
        values:
        - c
        - m
        - r
      - key: eks.amazonaws.com/instance-generation
        operator: Gt
        values:
        - "4"
      - key: kubernetes.io/arch
        operator: In
        values:
        - amd64
      - key: kubernetes.io/os
        operator: In
        values:
        - linux
      terminationGracePeriod: 24h0m0s`

The `WhenEmptyOrUnderutilized` configuration property ensures that Karpenter will consider all nodes for consolidation and attempt to remove or replace nodes when it discovers that a node is empty or underutilized and could be removed or replaced to reduce cost. `expireAfter` is set to a custom value so that nodes are terminated automatically after 336 hours (14 days). The `budget` configuration block control the speed Karpenter can scale down nodes.

## **Horizontal Pod Autoscaling**

In this lab, we'll explore how the Horizontal Pod Autoscaler (HPA) automatically scales pods in Kubernetes based on observed metrics. The HPA consists of a resource definition and a controller, where the controller periodically checks resource utilization (like CPU, memory, or custom metrics) against user-defined targets and adjusts the number of replicas accordingly.

The Metrics Server component is required to collect and aggregate the resource usage data from the cluster, and provide HPA with the necessary metrics to make scaling decisions.

[**Install Metrics Server**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/30-autoscaling#install-metrics-server)

To enable application-level autoscaling in EKS Auto Mode, it's essential to install the Metrics Server. AWS offers a streamlined installation process for the Metrics Server through the [Community Add-ons](https://docs.aws.amazon.com/eks/latest/userguide/community-addons.html)  to simplify deployment and management.

You can create an Amazon EKS add-on using `eksctl`, the AWS Management Console, or the AWS CLI. If the add-on requires an IAM role, see the details for the specific add-on in [Available Amazon EKS add-ons from AWS](https://docs.aws.amazon.com/eks/latest/userguide/workloads-add-ons-available-eks.html)  for details about creating the role.

[**Create add-on (eksctl)**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/30-autoscaling#create-add-on-(eksctl))

➤ Use `eksctl` to install the metrics-server addon:

`eksctl create addon --name metrics-server --cluster ${DEMO_CLUSTER_NAME}`

Creating the metrics-server add-on should take about 1 minute.

The output should look similar to the following:

`2025-01-16 00:06:09 [ℹ]  Kubernetes version "1.31" in use by cluster "eks-auto-workshop-cls-1"
2025-01-16 00:06:09 [ℹ]  creating addon
2025-01-16 00:07:00 [ℹ]  addon "metrics-server" active`

➤ After the above installation commands completes, let's confirm that the Metrics Server is running:

`kubectl get deployment metrics-server -n kube-system`

with the expected output:

`NAME             READY   UP-TO-DATE   AVAILABLE   AGE
metrics-server   2/2     2            2           99s`

To get a view of the metrics that HPA will use to drive its scaling behavior, use the `kubectl top` command.

➤ For example, the below commands will show the resource utilization of the nodes and UI component pods in our cluster:

`kubectl top node
kubectl top pods -l app.kubernetes.io/name=ui`

The result should be similar to the following:

`NAME                  CPU(cores)   CPU(%)   MEMORY(bytes)   MEMORY(%)
i-010ef666810cc74fe   20m          1%       589Mi           18%
i-014b2a0091dc49a40   19m          0%       586Mi           18%
i-0234821e6c1789b57   44m          2%       596Mi           19%
i-04eb412b3e09844ef   39m          2%       595Mi           19%
i-066e1d9c08f13c0ed   28m          1%       1670Mi          53%
i-06d0fd146733a2985   40m          2%       599Mi           19%
i-07c121b110f507617   45m          2%       597Mi           19%
i-0b87fcb18c6146df8   65m          3%       598Mi           19%
i-0c1cfed844ac873ea   36m          1%       1268Mi          40%
i-0db78db542f9b25da   55m          2%       603Mi           19%
i-0ed869e02ea7e95e4   11m          0%       599Mi           19%
i-0f8137d7076ba89f1   20m          1%       686Mi           22%
NAME                                  CPU(cores)   MEMORY(bytes)
retail-store-app-ui-697bbcdb5-2rcbq   1m           221Mi
retail-store-app-ui-697bbcdb5-hxgqp   1m           212Mi
retail-store-app-ui-697bbcdb5-jfdc6   1m           217Mi
retail-store-app-ui-697bbcdb5-jrtdm   2m           215Mi
retail-store-app-ui-697bbcdb5-kv79b   1m           221Mi
retail-store-app-ui-697bbcdb5-p99gf   1m           214Mi
retail-store-app-ui-697bbcdb5-qwpdb   1m           222Mi
retail-store-app-ui-697bbcdb5-sx4sp   2m           217Mi
retail-store-app-ui-697bbcdb5-wczzw   2m           226Mi
retail-store-app-ui-697bbcdb5-whxxf   2m           217Mi
retail-store-app-ui-697bbcdb5-zn667   1m           211Mi
retail-store-app-ui-697bbcdb5-zwhw8   1m           217Mi`

[**Configure HPA**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/30-autoscaling#configure-hpa)

Currently there are no resources in our cluster that enable Horizontal Pod Autoscaling.

➤ You can verify that by executing the following command:

`kubectl get hpa --all-namespaces`

with the expected output:

`No resources found`

Now, we are going to add autoscaling configurations to the UI component based on its CPU usage. For this, let's update our `values-ui.yaml` file with `autoscaling` config and re-deploy the UI component using the corresponding Helm chart.

[**Configure and re-deploy the UI component**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/30-autoscaling#configure-and-re-deploy-the-ui-component)

`helm upgrade -i retail-store-app-ui oci://public.ecr.aws/aws-containers/retail-store-sample-ui-chart \
  --version ${RETAIL_STORE_APP_HELM_CHART_VERSION} --hide-notes -f - << EOF
endpoints:
  catalog: http://retail-store-app-catalog:80
  carts: http://retail-store-app-carts:80
  checkout: http://retail-store-app-checkout:80
  orders: http://retail-store-app-orders:80
  assets: http://retail-store-app-assets:80

topologySpreadConstraints:
  - maxSkew: 1
    minDomains: 3
    topologyKey: topology.kubernetes.io/zone
    whenUnsatisfiable: DoNotSchedule
    labelSelector:
      matchLabels:
        app.kubernetes.io/name: ui
  - maxSkew: 1
    topologyKey: kubernetes.io/hostname
    whenUnsatisfiable: ScheduleAnyway
    labelSelector:
      matchLabels:
        app.kubernetes.io/instance: retail-store-app-ui

autoscaling:
  enabled: true
  minReplicas: 3
  maxReplicas: 10
  targetCPUUtilizationPercentage: 80
EOF`

The result should be similar to the following:

`Pulled: public.ecr.aws/aws-containers/retail-store-sample-ui-chart:0.8.5
Digest: sha256:3862f8ecac30a8cecc0825f5a654c2a8e31871b0342ffe3b5a84b1db1e10a7dd
Release "retail-store-app-ui" has been upgraded. Happy Helming!
NAME: retail-store-app-ui
LAST DEPLOYED: Fri Jan 17 15:13:18 2025
NAMESPACE: default
STATUS: deployed
REVISION: 3`

The HPA resource will always run at least 3 replica and will scale up to 10 replicas when the average CPU Utilization reaches 80%.

➤ View the HPA resource with the following command:

`kubectl get hpa`

The expected output should be similar to this:

`NAME                  REFERENCE                        TARGETS       MINPODS   MAXPODS   REPLICAS   AGE
retail-store-app-ui   Deployment/retail-store-app-ui   cpu: 2%/80%   3         10        3          13m`

[**Generate load**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/30-autoscaling#generate-load)

To observe HPA scale out in response to the policy, we have configured we need to generate some load on our application. We'll do that by calling the home page of the workload with [hey](https://github.com/rakyll/hey) .

The command below will run the load generator as a Pod in the cluster with:

- 10 workers running concurrently
- Sending 5 queries per second each
- Running for a maximum of 60 minutes

➤ Apply the load:

`kubectl run load-generator \
 --image=williamyeh/hey:latest \
 --restart=Never -- -c 10 -q 10 -z 3m http://retail-store-app-ui/utility/stress/100000`

Now that we have requests hitting our application we can watch the HPA resource to follow its progress.

➤ Execute the following command:

`kubectl get hpa retail-store-app-ui --watch`

The output should be similar to:

`NAME                  REFERENCE                        TARGETS       MINPODS   MAXPODS   REPLICAS   AGE
retail-store-app-ui   Deployment/retail-store-app-ui   cpu: 5%/80%   3         10        3          33m
retail-store-app-ui   Deployment/retail-store-app-ui   cpu: 6%/80%   3         10        3          33m
retail-store-app-ui   Deployment/retail-store-app-ui   cpu: 164%/80%   3         10        3          33m
retail-store-app-ui   Deployment/retail-store-app-ui   cpu: 139%/80%   3         10        6          33m
retail-store-app-ui   Deployment/retail-store-app-ui   cpu: 223%/80%   3         10        7          33m
retail-store-app-ui   Deployment/retail-store-app-ui   cpu: 258%/80%   3         10        10         34m
retail-store-app-ui   Deployment/retail-store-app-ui   cpu: 49%/80%    3         10        10         34m
retail-store-app-ui   Deployment/retail-store-app-ui   cpu: 70%/80%    3         10        10         34m`

You can see in the output above how the CPU utilization gradually grows with the load and causes HPA to add more replicas of the UI component to accommodate that load.

➤ You can watch the Pods scaling by executing the following command:

`watch kubectl get pods -l app.kubernetes.io/instance=retail-store-app-ui`

➤ You can also view, in another VS Code terminal, how EKS Auto Mode adds more nodes to host these replicas:

`watch kubectl get nodes`

➤ Once you're satisfied with the autoscaling behavior, you can end the watch with `Ctrl+C` and stop the load generator like so:

`kubectl delete pod load-generator`

---

## **Summary**

In this lab, we explored EKS Auto Mode's scaling capabilities through two main features: Karpenter's node-level disruption management and consolidation, and pod-level Horizontal Pod Autoscaling (HPA). We implemented and tested these features by leveraging the `general-purpose` NodePool's consolidation policies, setting up HPA for our UI application with specific scaling thresholds, and demonstrated automatic scaling in action using a load generator to trigger scale-out events.

In the next section, we will focus on compute customization in EKS Auto Mode. We'll explore how to optimize both performance and cost by configuring specific compute requirements for our applications using Graviton and Spot Instances.

# Customization

Amazon EKS Auto Mode offers powerful compute customization capabilities that enable you to optimize both performance and cost efficiency for your applications.

In this section, we'll explore how to leverage [AWS Graviton](https://aws.amazon.com/ec2/graviton/)  processors for enhanced price-performance benefits and implement Spot instances for significant cost savings.

By combining these strategies, you'll learn to configure your workloads to run on cost-effective compute resources while maintaining reliable performance.

We'll migrate application components to Graviton-based instances and implement Spot instance handling for fault-tolerant workloads, showcasing how EKS Auto Mode intelligently manages these compute resources to maximize efficiency and minimize operational costs.

# Graviton

[Overview](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/40-customization/10-graviton#overview) | [Create a Graviton NodePool](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/40-customization/10-graviton#create-graviton-nodepool) | [Summary](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/40-customization/10-graviton#summary)

---

This section will guide you through the basics of EKS Auto Mode compute customization options and explain in detail customization using Graviton.

## **Overview**

[**Graviton instances**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/40-customization/10-graviton#graviton-instances)

[AWS Graviton-based processors](https://aws.amazon.com/ec2/graviton/)  deliver the best price-performance for cloud workloads and offer up to a 40% better price-performance over comparable x86-based Amazon EC2 instances. Graviton processors also use up to 60% less energy than comparable EC2 instances for the same performance. AWS Graviton-based Amazon EC2 instances provide the best price-performance for a wide variety of Linux-based workloads, such as application servers, microservices, high-performance computing (HPC), CPU-based machine learning inference, video encoding, electronic design automation (EDA), gaming, open-source databases, in-memory caches, etc.

[**Review the current NodePool**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/40-customization/10-graviton#review-the-current-nodepool)

In this section, we will create a new, custom general purpose NodePool to provision AWS Graviton instances. Before we create the new NodePool, let's review the existing `general-purpose` NodePool and the current state of the nodes available in the cluster.

➤ Execute the following command:

`kubectl get nodepool general-purpose -o yaml`

The configuration of the `general-purpose` NodePool should look like this:

`apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
  annotations:
    karpenter.sh/nodepool-hash: "4012513481623584108"
    karpenter.sh/nodepool-hash-version: v3
  creationTimestamp: "2025-01-15T09:32:29Z"
  generation: 1
  labels:
    app.kubernetes.io/managed-by: eks
  name: general-purpose
  resourceVersion: "1097754"
  uid: 9b1c4ad0-d42d-4c63-bd96-b0a201aeec0e
spec:
  disruption:
    budgets:
    - nodes: 10%
    consolidateAfter: 30s
    consolidationPolicy: WhenEmptyOrUnderutilized
  template:
    metadata: {}
    spec:
      expireAfter: 336h
      nodeClassRef:
        group: eks.amazonaws.com
        kind: NodeClass
        name: default
      requirements:
      - key: karpenter.sh/capacity-type
        operator: In
        values:
        - on-demand
      - key: eks.amazonaws.com/instance-category
        operator: In
        values:
        - c
        - m
        - r
      - key: eks.amazonaws.com/instance-generation
        operator: Gt
        values:
        - "4"
      - key: kubernetes.io/arch
        operator: In
        values:
        - amd64
      - key: kubernetes.io/os
        operator: In
        values:
        - linux
      terminationGracePeriod: 24h0m0s
status:
  conditions:
  - lastTransitionTime: "2025-01-15T09:32:43Z"
    message: ""
    observedGeneration: 1
    reason: ValidationSucceeded
    status: "True"
    type: ValidationSucceeded
  - lastTransitionTime: "2025-01-15T09:32:44Z"
    message: ""
    observedGeneration: 1
    reason: NodeClassReady
    status: "True"
    type: NodeClassReady
  - lastTransitionTime: "2025-01-15T09:32:44Z"
    message: ""
    observedGeneration: 1
    reason: Ready
    status: "True"
    type: Ready
  resources:
    cpu: "4"
    ephemeral-storage: 163708Mi
    hugepages-1Gi: "0"
    hugepages-2Mi: "0"
    memory: 7717496Ki
    nodes: "2"
    pods: "54"`

➤ View the current instances processor architecture:

`kubectl get nodes -L kubernetes.io/arch`

with the corresponding output:

`NAME                  STATUS   ROLES    AGE   VERSION               ARCH
i-07c121b110f507617   Ready    <none>   15h   v1.31.3-eks-7636447   amd64
i-0c90d33aa6fccecff   Ready    <none>   16h   v1.31.3-eks-7636447   amd64`

The output above shows our existing nodes and their CPU architecture. All of the nodes are currently using EC2 instances with the **amd64** processor architecture as provisioned by the `general-purpose` NodePool.

Note that your output in the command above may be slightly different as EKS Auto Mode provisions instances within the requirements defined in the node pool above.

## **Create a Graviton NodePool**

Let's create a new NodePool that includes **arm64** (Graviton) for the `kubernetes.io/arch` requirement.

This will configure Auto Mode managed Karpenter to examine the `nodeAffinity` or `nodeSelector` of each new Pod to see if there's a specific CPU architecture requirement. Karpenter will launch a new Graviton node if it determines one is needed to fit pending pods. We will also add a taint for our Graviton NodePool to control the apps we want to schedule on these nodes. The taint will define the key and the effect to be `key:GravitonOnly` and `effect:NoSchedule`. This will ensure that only pods with the matching toleration will be scheduled on these nodes.

➤ Create the new NodePool definition:

`cat << EOF >~/environment/nodepool-graviton.yaml
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
  name: graviton
  labels:
    app.kubernetes.io/managed-by: app-team
spec:
  disruption:
    budgets:
    - nodes: 10%
    consolidateAfter: 30s
    consolidationPolicy: WhenEmptyOrUnderutilized
  template:
    metadata: {}
    spec:
      expireAfter: 336h
      nodeClassRef:
        group: eks.amazonaws.com
        kind: NodeClass
        name: default
      requirements:
      - key: karpenter.sh/capacity-type
        operator: In
        values:
        - on-demand
      - key: eks.amazonaws.com/instance-category
        operator: In
        values:
        - c
        - m
        - r
      - key: eks.amazonaws.com/instance-generation
        operator: Gt
        values:
        - "4"
      - key: kubernetes.io/arch
        operator: In
        values:
        - arm64
      taints:
      - effect: NoSchedule
        key: GravitonOnly
      terminationGracePeriod: 24h0m0s
  limits:
    cpu: "1000"
    memory: 1000Gi
EOF

kubectl apply -f ~/environment/nodepool-graviton.yaml`

This should result in this output:

`nodepool.karpenter.sh/graviton created`

[**Run pods on Graviton**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/40-customization/10-graviton#run-pods-on-graviton)

Now, that we have created our Graviton NodePool, we'll need to configure our application to take advantage of this change. To do so, let's configure our application to deploy the UI component on the `graviton` NodePool.

➤ Before making any changes, let's check the current configuration for the UI component pods.

`kubectl describe pod --selector app.kubernetes.io/name=ui`

This should produce an output similar to the following:

`Name:             retail-store-app-ui-697bbcdb5-jf6bs
Namespace:        default
Priority:         0
Service Account:  retail-store-app-ui
Node:             i-07c121b110f507617/20.0.144.196
Start Time:       Fri, 17 Jan 2025 15:17:29 +0000
Labels:           app.kuberneres.io/owner=retail-store-sample
                  app.kubernetes.io/component=service
                  app.kubernetes.io/instance=retail-store-app
                  app.kubernetes.io/name=ui
                  pod-template-hash=697bbcdb5
Annotations:      prometheus.io/path: /actuator/prometheus
                  prometheus.io/port: 8080
                  prometheus.io/scrape: true
Status:           Running
[...]
Node-Selectors:               <none>
Tolerations:                  node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                              node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Topology Spread Constraints:  kubernetes.io/hostname:ScheduleAnyway when max skew 1 is exceeded for selector app.kubernetes.io/name=ui
                              topology.kubernetes.io/zone:ScheduleAnyway when max skew 1 is exceeded for selector app.kubernetes.io/name=ui
Events:                       <none>`

The associated pod is in a `Running` status and we can confirm that no custom toleration have been configured.

Note that Kubernetes automatically adds toleration for `node.kubernetes.io/not-ready` and `node.kubernetes.io/unreachable` with `tolerationSeconds=300`, unless you or a controller set those toleration explicitly. These automatically-added toleration mean that Pods remain bound to nodes for 5 minutes after one of these problems is detected.

Let's update our UI component to bind its pods to our Graviton NodePool.

We've tainted the NodePool with `key:GravitonOnly` and it automatically adds a `karpenter.sh/nodepool` label.

The following `values-ui.yaml` describe the changes needed to our UI app configuration in order to enable this setup.

[**Re-deploy the UI component**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/40-customization/10-graviton#re-deploy-the-ui-component)

`cat << EOF >~/environment/values-ui.yaml
endpoints:
  catalog: http://retail-store-app-catalog:80
  carts: http://retail-store-app-carts:80
  checkout: http://retail-store-app-checkout:80
  orders: http://retail-store-app-orders:80
  assets: http://retail-store-app-assets:80

topologySpreadConstraints:
  - maxSkew: 1
    topologyKey: topology.kubernetes.io/zone
    whenUnsatisfiable: ScheduleAnyway
    labelSelector:
      matchLabels:
        app.kubernetes.io/name: ui

autoscaling:
  enabled: **false**
  minReplicas: 3
  maxReplicas: 10
  targetCPUUtilizationPercentage: 80

nodeSelector:
  karpenter.sh/nodepool: graviton
tolerations:
- key: "GravitonOnly"
  operator: "Exists"
EOF

helm upgrade -f ~/environment/values-ui.yaml retail-store-app-ui oci://public.ecr.aws/aws-containers/retail-store-sample-ui-chart --version ${RETAIL_STORE_APP_HELM_CHART_VERSION} --hide-notes`

Note that the UI component will fall back onto the original definitions in its `values-ui.yaml` file, which defined a single replica, which is what you should observe in the cluster.

This should produce the following output:

`Pulled: public.ecr.aws/aws-containers/retail-store-sample-ui-chart:0.8.5
Digest: sha256:5cd721c10214c306b06c7223367f626f21a8d471eee8f0a576742426f84141f2
Release "retail-store-app-ui" has been upgraded. Happy Helming!
NAME: retail-store-app-ui
LAST DEPLOYED: Sat Jan 18 23:54:22 2025
NAMESPACE: default
STATUS: deployed
REVISION: 4`

➤ Before checking the new Graviton nodes that should spin up, run the below command to ensure that all of the UI component pods are up and running:

`kubectl wait --for=condition=Ready pod -l app.kubernetes.io/instance=retail-store-app-ui --namespace default --timeout=300s`

➤ Now you can check the status of our EKS cluster nodes and UI component pods:

`kubectl get nodes -L kubernetes.io/arch -L karpenter.sh/nodepool
kubectl get pods -l app.kubernetes.io/name=ui -o wide`

With the expected output similar to the below:

`NAME                  STATUS   ROLES    AGE   VERSION               ARCH    NODEPOOL
i-07e57aa5210d22ebc   Ready    <none>   15m   v1.30.8-eks-3c20087   amd64   general-purpose
i-09142bb9a8dd413fa   Ready    <none>   15m   v1.30.8-eks-3c20087   amd64   general-purpose
i-09f0b5de0c31af315   Ready    <none>   85s   v1.30.8-eks-3c20087   arm64   graviton
NAME                                   READY   STATUS    RESTARTS   AGE    IP                NODE                  NOMINATED NODE   READINESS GATES
retail-store-app-ui-6cd4cd7b7b-hw82q   1/1     Running   0          112s   192.168.143.112   i-09f0b5de0c31af315   <none>           <none>`

As you can see, the UI component pods are now running on the Graviton NodePool. You can also see the taint on the node using the `kubectl describe node` command and the matching tolerations on the pods using the `kubectl describe pod` command.

---

[**Summary**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/40-customization/10-graviton#summary)

In this lab, we explored using AWS Graviton Instances in EKS Auto Mode for improved performance and cost efficiency.

We started by creating a dedicated Graviton NodePool that specifically requests arm64 architecture instances and includes a `GravitonOnly` taint for controlled pod scheduling. We then modified our application deployment by updating the UI component's configuration to include the necessary node selector and toleration, allowing it to run on Graviton instances.

In the next lab we will explore combining On-Demand Instances with Spot Instances for additional cost optimization.

# On-Demand & Spot

[Overview](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/40-customization/20-on-demand-spot-split#overview) | [Create NodePools](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/40-customization/20-on-demand-spot-split#create-nodepools) | [Deploy the application](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/40-customization/20-on-demand-spot-split#deploy-app) | [Summary](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/40-customization/20-on-demand-spot-split#summary)

---

This section will guide you through the basics of EKS Auto Mode and explain in detail Customization.

## **Overview**

All of our existing compute nodes are currently using On-Demand capacity. However, there are multiple [purchase options](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-purchasing-options.html)  available to EC2 customers for running their EKS workloads.

[Amazon EC2 Spot Instances](https://aws.amazon.com/ec2/spot/)  let you take advantage of unused EC2 capacity in the AWS cloud and are available at up to a 90% discount compared to On-Demand prices. You can use Spot Instances for various stateless, fault-tolerant, or flexible applications such as big data, containerized workloads, CI/CD, web servers, high-performance computing (HPC), and test & development workloads. EC2 Spot Instances are a cost-effective choice if you can be flexible about when your applications run and if your applications can be interrupted.

In this section, we will see how we can run workloads using both On-Demand and EC2 Spot instances with a desired ratio to guarantee the base availability of On-Demand nodes, while leveraging Spot instances for optimizing costs.

[**Create NodePools**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/40-customization/20-on-demand-spot-split#create-nodepools)

We will deploy two NodePools that will leverage Karpenter's ability to split workloads across on-demand and spot instance based on desired ratio.

➤ Execute the following command to create the NodePools:

`cat << EOF >~/environment/nodepool-ondemandspotsplit.yaml
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
  name: ondemand
  labels:
    app.kubernetes.io/managed-by: app-team
spec:
  disruption:
    consolidateAfter: 30s
    consolidationPolicy: WhenEmptyOrUnderutilized
  template:
    metadata:
      labels:
        EKSAutoNodePool: OnDemandSpotSplit
    spec:
      expireAfter: 336h
      nodeClassRef:
        group: eks.amazonaws.com
        kind: NodeClass
        name: default
      requirements:
      - key: eks.amazonaws.com/instance-category
        operator: In
        values:
        - c
        - m
        - r
      - key: eks.amazonaws.com/instance-generation
        operator: Gt
        values:
        - "4"
      - key: kubernetes.io/arch
        operator: In
        values:
        - amd64
      - key: karpenter.sh/capacity-type
        operator: In
        values:
        - on-demand
      - key: capacity-spread
        operator: In
        values:
        - "1"
      taints:
      - effect: NoSchedule
        key: OnDemandSpotSplit
      terminationGracePeriod: 24h0m0s
---
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
  name: spot
  labels:
    app.kubernetes.io/managed-by: app-team
spec:
  disruption:
    consolidateAfter: 30s
    consolidationPolicy: WhenEmptyOrUnderutilized
  template:
    metadata:
      labels:
        EKSAutoNodePool: OnDemandSpotSplit
    spec:
      expireAfter: 336h
      nodeClassRef:
        group: eks.amazonaws.com
        kind: NodeClass
        name: default
      requirements:
      - key: eks.amazonaws.com/instance-category
        operator: In
        values:
        - c
        - m
        - r
      - key: eks.amazonaws.com/instance-generation
        operator: Gt
        values:
        - "4"
      - key: kubernetes.io/arch
        operator: In
        values:
        - amd64
      - key: karpenter.sh/capacity-type
        operator: In
        values:
        - spot
      - key: capacity-spread
        operator: In
        values:
        - "2"
        - "3"
        - "4"
        - "5"
      taints:
      - effect: NoSchedule
        key: OnDemandSpotSplit
      terminationGracePeriod: 24h0m0s
EOF

kubectl apply -f ~/environment/nodepool-ondemandspotsplit.yaml`

The output should be similar:

`nodepool.karpenter.sh/ondemand created
nodepool.karpenter.sh/spot created`

Taking advantage of Karpenter’s ability to assign labels to a node and using a topology spread across those labels enables a crude method for splitting a workload across on-demand and spot instances in a desired ratio.

To do this, we created one NodePool each for Spot and On-Demand capacity types with disjoint values for a unique new label called `capacity-spread`. In the example above, we provide four unique values for the spot NodePool and one value for the On-Demand NodePool. When we spread across our new label evenly, we’ll end up with a ratio of 4:1 spot to On-Demand nodes.

## **Deploy the application**

In this lab, we will use the `catalog` component to run its replicas on Spot Instances. Let's configure our catalog application deployment with 5 replicas. Using the capacity-spread label, we will spread across our new label evenly, we’ll end up with a ratio of 4:1 spot to On-Demand nodes.

[**Configure and re-deploy the `catalog` component**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/40-customization/20-on-demand-spot-split#configure-and-re-deploy-the-catalog-component)

➤ Configure and re-deploy the component:

`cat << EOF >~/environment/values-catalog.yaml
replicaCount: 5
  
topologySpreadConstraints:
  - maxSkew: 1
    minDomains: 5
    topologyKey: capacity-spread
    whenUnsatisfiable: DoNotSchedule
    labelSelector:
      matchLabels:
        app.kubernetes.io/name: catalog

nodeSelector:
  EKSAutoNodePool: OnDemandSpotSplit
tolerations:
- key: "OnDemandSpotSplit"
  operator: "Exists"
EOF

helm upgrade -f ~/environment/values-catalog.yaml retail-store-app-catalog oci://public.ecr.aws/aws-containers/retail-store-sample-catalog-chart --version ${RETAIL_STORE_APP_HELM_CHART_VERSION} --hide-notes`

The output should be similar to:

`Pulled: public.ecr.aws/aws-containers/retail-store-sample-catalog-chart:0.8.5
Digest: sha256:0dc16ac63a8f32f309ea7d69f58973520c156305f69f2703fcb5564da6b67eb6
Release "retail-store-app-catalog" has been upgraded. Happy Helming!
NAME: retail-store-app-catalog
LAST DEPLOYED: Sun Jan 19 23:42:07 2025
NAMESPACE: default
STATUS: deployed
REVISION: 2`

Finally, we can verify that the `catalog` component pods are running on Spot instances.

➤ Run the following commands to check the nodes and pods:

`kubectl get node -L karpenter.sh/capacity-type --no-headers | while read node status roles age version capacity_type; do
echo "Pods on node $node (Capacity Type: $capacity_type):"
  kubectl get pods --all-namespaces --field-selector spec.nodeName=$node -l app.kubernetes.io/instance=retail-store-app-catalog
echo "-----------------------------------"
done`

Note that it may take a minute for the instances to be created and operational.

`Pods on node i-02e25edfdcf052a8d (Capacity Type: on-demand):
No resources found
-----------------------------------
Pods on node i-059c896e2ddc3787f (Capacity Type: spot):
NAMESPACE   NAME                                        READY   STATUS    RESTARTS   AGE
default     retail-store-app-catalog-7568d4cffb-svztn   1/1     Running   0          2m13s
-----------------------------------
Pods on node i-074da6ae5127bf5dd (Capacity Type: on-demand):
No resources found
-----------------------------------
Pods on node i-0865727e5109e8eda (Capacity Type: on-demand):
NAMESPACE   NAME                                        READY   STATUS    RESTARTS   AGE
default     retail-store-app-catalog-7568d4cffb-ft88b   1/1     Running   0          2m16s
-----------------------------------
Pods on node i-095f16c14ff78d4e0 (Capacity Type: spot):
NAMESPACE   NAME                                        READY   STATUS    RESTARTS   AGE
default     retail-store-app-catalog-7568d4cffb-gkvqj   1/1     Running   0          2m59s
-----------------------------------
Pods on node i-0995ee2810f2eda4b (Capacity Type: on-demand):
No resources found
-----------------------------------
Pods on node i-0b36d75cd120def01 (Capacity Type: spot):
NAMESPACE   NAME                                        READY   STATUS    RESTARTS   AGE
default     retail-store-app-catalog-7568d4cffb-s6t4f   1/1     Running   0          3m2s
-----------------------------------
Pods on node i-0d7d6046307eecb7e (Capacity Type: spot):
NAMESPACE   NAME                                        READY   STATUS    RESTARTS   AGE
default     retail-store-app-catalog-7568d4cffb-4n4xs   1/1     Running   0          3m3s`

You can see that the `catalog` app pods are spread across Spot and On-demand capacity types

---

## **Summary**

In this lab, we explored how to leverage both On-Demand and Spot instances in EKS Auto Mode. We implemented a split-ratio strategy by creating two NodePools - one for On-Demand instances and another for Spot instances using `capacity-spread` label. We configured the Spot NodePool with four unique spread values and the On-Demand NodePool with one value, effectively creating a 4:1 ratio of Spot to On-Demand instances.

To demonstrate this configuration, we configured our catalog application with 5 replicas and used topology spread constraints to distribute the pods across the nodes according to our desired ratio. This approach allows organizations to maintain a baseline of stable On-Demand capacity while taking advantage of cost-effective Spot instances for interruption-tolerant workloads.

The lab successfully showed how to achieve a balance between reliability and cost optimization in EKS cluster management.

# Networking

EKS Auto Mode supports several network capabilities that are important for security, cluster operations, and application connectivity inside and outside of the cluster.

This section will cover how to expose applications using Network Load Balancer and Application Load Balancer.

# Exposing Applications

[Overview](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/20-networking/10-exposing-applications#overview) | [Expose the application](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/20-networking/10-exposing-applications#expose-app) | [Summary](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/20-networking/10-exposing-applications#summary)

---

## **Overview**

In this hands-on lab, you'll learn how to expose applications in Amazon EKS Auto Mode using AWS's managed load balancing solutions.

You will work through a practical scenario to:

- Configure an Application Load Balancer (ALB) using Kubernetes Ingress resources
- Set up a Network Load Balancer (NLB) using Kubernetes Service resources
- Implement path-based routing to share a single ALB across multiple services
- Observe load balancing in action with custom response headers showing which pods handle requests

## **Expose the application**

EKS Auto Mode simplifies the process by automatically managing the lifecycle of the ALBs and NLBs that are required for your application. As EKS Auto Mode is Kubernetes conformant, it allows you to use the same Kubernetes constructs of [Service](https://kubernetes.io/docs/concepts/services-networking/service/)  and [Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/)  to provision those Load Balancers.

In the remainder of this module, you'll learn how to provision those load balancers with Auto Mode.

[**Step 1: Set Up IngressClass for ALB**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/20-networking/10-exposing-applications#step-1:-set-up-ingressclass-for-alb)

Since Ingresses can be implemented by different controllers, each Ingress should specify a class, a reference to an IngressClass resource that contains additional configuration including the name of the controller that should implement the class.

IngressClass resources contain an optional parameters field. This can be used to reference additional implementation-specific configuration for this class.

To target the EKS Auto Mode ALB load balancing capability controller, you will create an `IngressClassParams`, which allows you to define an AWS specific configuration for your ALB such as certificates to use, the subnets to use for the ALB ENIs, or the [ingress group](https://kubernetes-sigs.github.io/aws-load-balancer-controller/v2.11/guide/ingress/annotations/#ingressgroup)  configuration to group together multiple ingress objects into a single ALB.

The supported configurations for the `IngressClassParams` objects are [listed](https://docs.aws.amazon.com/eks/latest/userguide/auto-configure-alb.html#ingress-reference)  in EKS Auto Mode documentation. Additionally, you will create `IngressClass` that will use the `IngressClassParams` and point to the EKS Auto Mode capability. This is a one-time setup required for using ALBs in your cluster. Notice the `spec.controller` definition in the IngressClass below.

➤ Create the IngressClass and IngressClassParams to further configure the EKS Auto Mode load balancing capability:

`cat << EOF >~/environment/ingress.yaml
apiVersion: eks.amazonaws.com/v1
kind: IngressClassParams
metadata:
  name: eks-auto-alb
spec:
  scheme: internet-facing
---
apiVersion: networking.k8s.io/v1
kind: IngressClass
metadata:
  name: eks-auto-alb
  annotations:
    ingressclass.kubernetes.io/is-default-class: "true"
spec:
  controller: eks.amazonaws.com/alb
  parameters:
    apiGroup: eks.amazonaws.com
    kind: IngressClassParams
    name: eks-auto-alb
EOF

kubectl apply -f ~/environment/ingress.yaml`

This should produce the following output:

`ingressclassparams.eks.amazonaws.com/eks-auto-alb created
ingressclass.networking.k8s.io/eks-auto-alb created`

➤ Verify that the resources have been created:

`kubectl get ingressclass,ingressclassparams`

The output should look like the one below:

`NAME                                          CONTROLLER              PARAMETERS                                          AGE
ingressclass.networking.k8s.io/eks-auto-alb   eks.amazonaws.com/alb   IngressClassParams.eks.amazonaws.com/eks-auto-alb   56s

NAME                                                GROUP-NAME   SCHEME            IP-ADDRESS-TYPE   AGE
ingressclassparams.eks.amazonaws.com/eks-auto-alb                internet-facing                     56s`

Note the controller used, as well as the `SCHEME` defined (`internet-facing` in our case) which is based on our configuration above.

[**Step 2: Deploy the Retail Store Application**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/20-networking/10-exposing-applications#step-2:-deploy-the-retail-store-application)

You will now update the UI component to provision an ALB by creating an Ingress object, as you can see with the `ingress` configuration in the component's Helm chart values.

➤ Re-deploy the UI component with custom values:

`helm upgrade -i retail-store-app-ui oci://public.ecr.aws/aws-containers/retail-store-sample-ui-chart \
  --version ${RETAIL_STORE_APP_HELM_CHART_VERSION} --hide-notes -f - << EOF
endpoints:
  catalog: http://retail-store-app-catalog.default:80
  carts: http://retail-store-app-carts.default:80
  checkout: http://retail-store-app-checkout.default:80
  orders: http://retail-store-app-orders.default:80
  assets: http://retail-store-app-assets.default:80

autoscaling:
  enabled: **false**
  minReplicas: 1
  maxReplicas: 10
  targetCPUUtilizationPercentage: 80

topologySpreadConstraints:

   - maxSkew: 1
     minDomains: 3
     topologyKey: topology.kubernetes.io/zone
     whenUnsatisfiable: DoNotSchedule
     labelSelector:
       matchLabels:
         app.kubernetes.io/name: ui

ingress:
  enabled: **true**
  className: eks-auto-alb
  annotations:
    alb.ingress.kubernetes.io/healthcheck-path: /actuator/health/liveness
    alb.ingress.kubernetes.io/healthcheck-interval-seconds: '15'
    alb.ingress.kubernetes.io/healthcheck-timeout-seconds: '5'
    alb.ingress.kubernetes.io/healthy-threshold-count: '2'
    alb.ingress.kubernetes.io/unhealthy-threshold-count: '2'
    alb.ingress.kubernetes.io/success-codes: '200-399'
EOF`

This should produce an output similar to the following:

`Pulled: public.ecr.aws/aws-containers/retail-store-sample-ui-chart:0.8.5
Digest: sha256:5cd721c10214c306b06c7223367f626f21a8d471eee8f0a576742426f84141f2
Release "retail-store-app-ui" has been upgraded. Happy Helming!
NAME: retail-store-app-ui
LAST DEPLOYED: Sun Feb 16 21:30:01 2025
NAMESPACE: default
STATUS: deployed
REVISION: 5`

➤ Wait for all deployments to be ready by using the following command:

`kubectl wait --for=condition=available deployments retail-store-app-ui --all`

Example output:

`deployment.apps/retail-store-app-ui condition met`

[**Step 3: Access the UI application with the provisioned ALB**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/20-networking/10-exposing-applications#step-3:-access-the-ui-application-with-the-provisioned-alb)

The Ingress object that you've deployed in the previous step, gets translated by EKS Auto Mode into ALB with the appropriate configurations you've defined in the Ingress object itself, and in the IngressClassParams above.

➤ Retrieve the ALB's DNS endpoint by executing the following command:

`export ALB_URL=$(kubectl get ingress retail-store-app-ui -o jsonpath='{.status.loadBalancer.ingress[0].hostname}')
echo "Your application is available at: http://${ALB_URL}"`

**ALB provisioning takes couple of minutes**

Note that ALB provision and targets registration may take several minutes.

At this point, you can use the URL to access the application in a new browser window.

**Accessing the app**

If you're experiencing 500 HTTP error from the UI app, this might be because the `catalog` component didn't bootstrap properly (as it uses local data, and not an actual EBS volume which you'll get to experiment with in the next section). To fix it, simply restart the deployment of the catalog app by running the following command:

`kubectl rollout restart deployment retail-store-app-catalog`

[**Step 4: Expose Catalog Service Using NLB**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/20-networking/10-exposing-applications#step-4:-expose-catalog-service-using-nlb)

In the previous steps, you've used EKS Auto Mode to provision an ALB. You'll now experience how to use EKS Auto Mode to provision NLB using the Kubernetes `Service` object.

➤ Execute the following command.

`1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
kubectl apply -f - << EOF
apiVersion: v1
kind: Service
metadata:
  name: catalog-nlb
  annotations:
    service.beta.kubernetes.io/aws-load-balancer-type: "external"
    service.beta.kubernetes.io/aws-load-balancer-nlb-target-type: "ip"
    service.beta.kubernetes.io/aws-load-balancer-scheme: "internet-facing"
spec:
  type: LoadBalancer
  ports:
    - port: 80
      targetPort: http
      protocol: TCP
  selector:
    app.kubernetes.io/name: catalog
EOF`

➤ Wait for the NLB to be provisioned and get its URL:

`export NLB_URL=$(kubectl get service catalog-nlb -o jsonpath='{.status.loadBalancer.ingress[0].hostname}')
echo "The catalog service is also available at: http://${NLB_URL}"`

[**Step 5: Test Load Balancer Access**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/20-networking/10-exposing-applications#step-5:-test-load-balancer-access)

Let's test access to your application and observe load balancing in action. The `catalog` service has been configured with 5 replicas in the compute module under ["On-Demand & Spot Split Ratio"](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/10-compute/40-customization/20-on-demand-spot-split.md). You will use this to demonstrate load distribution.

➤ First, verify that all `catalog` pods are running:

`kubectl get pods -l app.kubernetes.io/name=catalog,app.kubernetes.io/component=service`

You should see that all of the `catalog`'s component pods are in `Running` state. Now, let's use two terminal windows to observe the load balancing behavior.

➤ In your first terminal, watch the logs from all `catalog` pods:

`kubectl logs -f -l app.kubernetes.io/name=catalog,app.kubernetes.io/component=service --prefix=true`

➤ In your second terminal, generate some traffic through the ALB:

`# Get the ALB URL
export ALB_URL=$(kubectl get ingress retail-store-app-ui -o jsonpath='{.status.loadBalancer.ingress[0].hostname}')
echo "The application is available at: http://${ALB_URL}"

# Generate traffic to see load balancing across pods
CURL_CMD=$(which curl)
for i in {1..15}; do
  echo "Sending request $i..."
  $CURL_CMD -s "http://${ALB_URL}/catalog?request=$i" > /dev/null
  sleep 2
done`

You should see detailed logs in your first terminal showing requests being distributed across all three catalog pods. Each log line shows:

- Which pod handled the request (in the prefix)
- HTTP method and path
- Response status code
- Request processing time
- Client IP address

Example log output showing distribution across pods:

`[pod/retail-store-app-catalog-7d8748bc8d-bzq65/catalog] [GIN] 2025/01/30 - 12:33:45 | 200 | 584.373µs | 192.168.139.174 | GET "/catalogue/tags"
[pod/retail-store-app-catalog-7d8748bc8d-77c2t/catalog] [GIN] 2025/01/30 - 12:34:17 | 200 | 52.413ms | 192.168.139.173 | GET "/catalogue/size?tags="
[pod/retail-store-app-catalog-7d8748bc8d-tkdqm/catalog] [GIN] 2025/01/30 - 12:34:17 | 200 | 16.882ms | 192.168.140.179 | GET "/catalogue?tags=&order=&page=1&size=4"`

Notice the highlighted lines showing different pod suffixes (`bzq65`, `77c2t`, `tkdqm`) handling the requests, demonstrating the load balancing distribution.

The catalog service uses the Gin web framework which provides detailed request logging. You can observe:

- Requests being distributed across different pods (see the pod names in the log prefix)
- Multiple requests being made for each page load (tags, size, and catalog data)
- Response times for each request
- Client IPs making the requests

[**Step 6: Share ALB Across Multiple Services - Multiple Ingress Pattern**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/20-networking/10-exposing-applications#step-6:-share-alb-across-multiple-services-multiple-ingress-pattern)

In some use-cases you need to ensure that multiple ingress objects doesn't create multiple ALBs but rather use the same ALB with multiple routing rules. This is where EKS Auto Mode supports ingress grouping using the IngressClassParams object (see reference in the [documentation](https://docs.aws.amazon.com/eks/latest/userguide/auto-configure-alb.html#ingress-reference) ). In this step you will create a new `IngressClass` object with new `IngressClassParams` that supports such grouping. For demonstration purposes you will then create 2 ingress objects: one for the `ui` component and one for the `catalog` service. With this configuration, since you've configured the grouping on the IngressClassParams, a single ALB will be created pointing to 2 of those services. Follow the steps below to achieve that:

➤ 1. Create a new IngressClassParams and IngressClass with `group.name` configuration:

`cat << EOF >~/environment/ingress-class-group.yaml
apiVersion: eks.amazonaws.com/v1
kind: IngressClassParams
metadata:
  name: eks-auto-alb-group-retail
spec:
  scheme: internet-facing
  group:
    name: retail
---
apiVersion: networking.k8s.io/v1
kind: IngressClass
metadata:
  name: eks-auto-alb-group-retail
  annotations:
    ingressclass.kubernetes.io/is-default-class: "true"
spec:
  controller: eks.amazonaws.com/alb
  parameters:
    apiGroup: eks.amazonaws.com
    kind: IngressClassParams
    name: eks-auto-alb-group-retail
EOF

kubectl apply -f ~/environment/ingress-class-group.yaml`

➤ 2. Create an ingress object for the `ui` component (note the use of the newly created IngressClass `eks-auto-alb-group-retail` ):

`kubectl apply -f - << EOF
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: retail-store-shared-group-ui
  annotations:
    alb.ingress.kubernetes.io/target-type: ip
    alb.ingress.kubernetes.io/healthcheck-path: /actuator/health/liveness
spec:
  ingressClassName: eks-auto-alb-group-retail
  rules:
    - http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: retail-store-app-ui
                port:
                  number: 80
EOF`

➤ 3. Create a second ingress object for the `catalog` component:

`kubectl apply -f - << EOF
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: retail-store-shared-group-catalog
  annotations:
    alb.ingress.kubernetes.io/target-type: ip
    alb.ingress.kubernetes.io/healthcheck-path: /health
spec:
  ingressClassName: eks-auto-alb-group-retail
  rules:
  - http:
      paths:
      - path: /catalogue
        pathType: Prefix
        backend:
          service:
            name: retail-store-app-catalog
            port:
              number: 80
EOF`

➤ 4. Verify the ingresses had been created:

`kubectl get ingress`

Note that the output `ADDRESS` of both ingresses of the `catalog` and the `ui` has the same DNS. This is because of the IngressClassParams group configuration you've used above.

`NAME                                 CLASS                       HOSTS   ADDRESS                                                                 PORTS   AGE
retail-store-app-ui                  eks-auto-alb                *       k8s-default-retailst-70051948b0-467757540.us-west-2.elb.amazonaws.com   80      16m
retail-store-backend-group-catalog   eks-auto-alb-group-retail   *       k8s-retail-5620a3cc93-1836759971.us-west-2.elb.amazonaws.com            80      30s
retail-store-backend-group-ui        eks-auto-alb-group-retail   *       k8s-retail-5620a3cc93-1836759971.us-west-2.elb.amazonaws.com            80      11m`

➤ 5. Extract the ALB DNS (note that because both ingresses has the same DNS, we can randomly choose one of them):

`# Get the shared ALB URL
export SHARED_ALB_URL=$(kubectl get ingress retail-store-shared-group-ui -o jsonpath='{.status.loadBalancer.ingress[0].hostname}')
echo "The shared ALB is available at: http://$SHARED_ALB_URL"`

The ALB load balancer creation process can take couple of minutes including its DNS to propagate so you will be able to test it.

➤ 6. Use the extracted DNS to access both services through a single ALB. You should expect an HTML output from the `/` path (coming from the `ui` component), and a list of items when hitting the `/catalogue` path, coming from `catalog` component:

`# Get the Shared ALB URL
export SHARED_ALB_URL=$(kubectl get ingress retail-store-shared-group-ui -o jsonpath='{.status.loadBalancer.ingress[0].hostname}')
echo "The shared ALB is available at: http://$SHARED_ALB_URL"

# Test each shared service endpoint
echo "Testing / endpoint accessing the ui component..."
curl -s "http://$SHARED_ALB_URL/" 

echo "Testing /catalog endpoint accessing the catalog component..."
curl -s "http://$SHARED_ALB_URL/catalogue" | jq`

---

## **Summary**

In this lab, you've learned how to:

- Deploy a real-world microservices application on EKS Auto Mode
- Set up ALB ingress for both frontend and backend services
- Use path-based routing to organize your microservices
- Observe load balancing across multiple pods

Remember that EKS Auto Mode manages the underlying load balancer infrastructure, but you still need to define the desired state through Kubernetes resources.

For production environments:

- Use HTTPS/TLS termination for security
- Implement proper health checks for your services
- Consider using AWS WAF for additional security
- Monitor your ALB metrics in CloudWatch
- Configure appropriate timeouts and connection settings for your Spring Boot services
- Set up proper logging and monitoring for your microservices
- Consider implementing circuit breakers and fallbacks

# EBS Storage

A StorageClass in Amazon EKS Auto Mode defines how Amazon EBS volumes are automatically provisioned when applications request persistent storage. By configuring a StorageClass, you can specify default settings for your EBS volumes including volume type, encryption, IOPS, and other storage parameters. You can also configure a StorageClass to use AWS KMS keys for encryption management.

In this section you will learn to create and configure StorageClass resources that works with Amazon EKS Auto Mode to provision EBS volumes.

# StatefulSets and PersistentVolumes

[Overview](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/30-storage/10-stateful-sets-persistent-volumes#overview) | [Inspect SQL databases](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/30-storage/10-stateful-sets-persistent-volumes#inspect-dbs) | [Demonstrate the ephemeral nature of emptyDir](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/30-storage/10-stateful-sets-persistent-volumes#empty-dir) | [Summary](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/30-storage/10-stateful-sets-persistent-volumes#summary)

---

## **Overview**

The *catalog* and *order* microservices each utilize a SQL database running in a separate pod in the cluster. Before we dive deeper into how these are deployed, let us review a number of relevant Kubernetes concepts:

- A [Volume](https://kubernetes.io/docs/concepts/storage/volumes/)  is a data store which is accessible to the containers in a pod. How that data store comes to be, and the medium that backs it, are determined by the particular volume type used.
- An [Ephemeral Volume](https://kubernetes.io/docs/concepts/storage/ephemeral-volumes/)  follows a pod's lifetime, and gets created and deleted along with the pod.
- A [PersistentVolume](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)  (PV) is a piece of storage in the cluster that has been provisioned by an administrator or dynamically provisioned using a StorageClass. It is a resource in the cluster just like a node is a cluster resource. PVs are a special kind of Volume with a lifecycle independent of any individual pod that uses the PV.
- A [PersistentVolumeClaim](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims)  (PVC) is a request for persistent storage by a user. It is the storage equivalent of a pod, wherein pods consume node resources and PVCs consume PV resources. Just as pods can request specific levels of resources (CPU and Memory), claims can request specific size and access modes (e.g. they can be mounted ReadWriteOnce, ReadOnlyMany, ReadWriteMany, or ReadWriteOncePod).
- A [StatefulSet](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)  runs a group of pods, and maintains a sticky identity for each of those pods. Although individual pods in a StatefulSet are susceptible to failure, the persistent pod identifiers make it easier to match existing volumes to the new pods that replace any that have failed. This is useful for managing applications, such as databases, that need persistent storage.
- A [StorageClass](https://kubernetes.io/docs/concepts/storage/storage-classes/)  provides a way for administrators to describe a "class" of storage they offer. Different classes might map to quality-of-service levels, or to backup policies, or to arbitrary policies determined by cluster administrators.
- [Dynamic Volume Provisioning](https://kubernetes.io/docs/concepts/storage/dynamic-provisioning/)  allows storage volumes to be created on-demand. Without dynamic provisioning, cluster administrators have to manually make calls to their cloud or storage provider to create new storage volumes, and then create PersistentVolume objects to represent them in Kubernetes. The dynamic provisioning feature eliminates the need for cluster administrators to pre-provision storage. Instead, it automatically provisions storage when it is requested by users.

## **Inspect SQL databases**

The `catalog` microservice utilizes a MySQL database running in a pod in the cluster.

➤ You can inspect the MySQL database pod to see its current volume configuration:

`kubectl describe statefulset retail-store-app-catalog-mysql`

You should see output similar to the below:

`Name:               retail-store-app-catalog-mysql
Namespace:          default
...
Replicas:           1 desired | 1 total
...
Pod Template:
...
  Containers:
   mysql:
    Image:      public.ecr.aws/docker/library/mysql:8.0
    Port:       3306/TCP
    Host Port:  0/TCP
    Environment:
      MYSQL_ROOT_PASSWORD:  my-secret-pw
      MYSQL_DATABASE:       catalog
      MYSQL_USER:           <set to the key 'username' in secret 'catalog-db'> Optional: false
      MYSQL_PASSWORD:       <set to the key 'password' in secret 'catalog-db'>  Optional: false
    Mounts:
      /var/lib/mysql from data (rw)
  Volumes:
   data:
    Type:          EmptyDir (a temporary directory that shares a pod's lifetime)
    Medium:
    SizeLimit:     <unset>
  Node-Selectors:  <none>
  Tolerations:     <none>
Volume Claims:     <none>
...`

We can make the following observations:

- The MySQL database is deployed as a `StatefulSet` with a single replica.
- The pod template includes a single `mysql` container, with a `data` volume of type `emptyDir`.

Similarly the *orders* microservice utilizes a PostgreSQL database.

➤ You can inspect the PostgreSQL database pod to see its current volume configuration:

`kubectl describe statefulset retail-store-app-orders-postgresql`

You should see output similar to the below:

`Name:               retail-store-app-orders-postgresql
Namespace:          default
...
Replicas:           1 desired | 1 total
...
  Containers:
   postgresql:
    Image:      public.ecr.aws/docker/library/postgres:16.1
    Port:       5432/TCP
    Host Port:  0/TCP
    Environment:
      POSTGRES_DB:        orders
      POSTGRES_USER:      <set to the key 'username' in secret 'orders-db'>  Optional: false
      POSTGRES_PASSWORD:  <set to the key 'password' in secret 'orders-db'>  Optional: false
      PGDATA:             /data/pgdata
    Mounts:
      /data from data (rw)
  Volumes:
   data:
    Type:          EmptyDir (a temporary directory that shares a pod's lifetime)
    Medium:
    SizeLimit:     <unset>
  Node-Selectors:  <none>
  Tolerations:     <none>
Volume Claims:     <none>
Events:            <none>`

Once again, you can see that the PostgreSQL database is deployed as a `StatefulSet` with a single replica, and using a `data` volume of type `emptyDir`.

## **Demonstrate the ephemeral nature of `emptyDir`**

An `emptyDir` volume is first created when a Pod is assigned to a node, and exists as long as that Pod is running on that node. As the name implies, the `emptyDir` volume is initially empty. All containers in the Pod can read and write the same files in the `emptyDir` volume, though that volume can be mounted on the same or different paths in each container. When a pod is removed from a node for any reason, the data in the `emptyDir` is deleted permanently. Therefore `emptyDir` is not a good fit for our SQL databases.

We can demonstrate the ephemeral nature of `emptyDir` by starting a shell session inside the PostgreSQL container and creating a test file. After that we'll delete the pod that is running in our StatefulSet. Because the pod is using an `emptyDir` and not a PV, the file will not survive a pod restart.

➤ First let's run a command inside our PostgreSQL container to create a file in the `/data/pgdata` path (where PostgreSQL saves database files):

`kubectl exec retail-store-app-orders-postgresql-0 -- bash -c "echo 123 > /data/pgdata/test.txt"`

➤ Now, let's verify our `test.txt` file was created in the `/data/pgdata` directory:

`kubectl exec retail-store-app-orders-postgresql-0 -- cat /data/pgdata/test.txt`

You should see the contents of the file we created:

`123`

➤ Now, let's remove the current `retail-store-app-orders-postgresql` pod to force the `StatefulSet` controller to automatically re-create a new `retail-store-app-orders-postgresql` pod:

`kubectl delete pod retail-store-app-orders-postgresql-0`

➤ Wait for the pod to be re-created:

`kubectl wait --for=condition=Ready pod retail-store-app-orders-postgresql-0 --timeout=30s`

After a few seconds you should see:

`pod/retail-store-app-orders-postgresql-0 condition met`

➤ Verify the pod is running:

`kubectl get pod retail-store-app-orders-postgresql-0`

The output should be similar to the following:

`NAME                                   READY   STATUS    RESTARTS   AGE
retail-store-app-orders-postgresql-0   1/1     Running   0          48s`

➤ Check for the presence of `test.txt` in the `/data/pgdata` directory:

`kubectl exec retail-store-app-orders-postgresql-0 -- cat /data/pgdata/test.txt`

With the following output:

`cat: /data/pgdata/test.txt: No such file or directory
command terminated with exit code 1`

You can see that the `test.txt` file no longer exists due to `emptyDir` volumes being ephemeral.

---

## **Summary**

In this section, you performed the following steps:

- Inspected the `StatefulSet` resources associated with the *catalog* MySQL database and the *orders* PostgreSQL database.
- Verified that these databases are both provisioned using `emptyDir` volumes.
- Demonstrated the ephemeral nature of `emptyDir` volumes.

In the next section, you will define a default `StorageClass` and use this to create a persistent volume for the *catalog* MySQL database.

# Default Storage Class using EBS CSI driver

[Overview](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/30-storage/20-storage-class#overview) | [Update the components](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/30-storage/20-storage-class#update-components) | [Summary](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/30-storage/20-storage-class#summary)

## **Overview**

In the previous section we saw that the databases for the `catalog` and `orders` services are using ephemeral `emptyDir` volumes for storage. In the remainder of this module, you will create a `StorageClass` which you then use to replace these volumes with persistent volumes using the EBS CSI driver. You will also learn how you can use the `StorageClass` to configure a volume parameter, such as a KMS key to encrypt the volume.

In this section you will create a default `StorageClass` and use this to create a persistent volume for the `catalog` MySQL database. In the next section, you will then create an additional `StorageClass` for the `orders` PostgreSQL database which increases the amount of provisioned IOPS.

## **Update the components**

[**Create a default StorageClass with KMS encryption**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/30-storage/20-storage-class#create-a-default-storageclass-with-kms-encryption)

➤ First, create a KMS key as follows:

`KEY_ID=$(aws kms create-key --tags TagKey=Name,TagValue=eks-automode-workshop --query 'KeyMetadata.KeyId' --output text)
KEY_ARN=$(aws kms describe-key --key-id $KEY_ID --query 'KeyMetadata.Arn' --output text)
echo "Key Id:" $KEY_ID
echo "Key Arn:" $KEY_ARN`

➤ Next, create an IAM resource policy JSON document for the KMS key, which allows the CSI service that runs on the EC2 managed instance, to assume that role to encrypt & decrypt the data written to the EBS volume:

`AWS_ACCOUNT_ID=$(aws sts get-caller-identity --query Account --output text)
AWS_REGION=$(aws configure list | grep region | awk '{print $2}')
cat >key-policy.json <<EOF
{
    "Version": "2012-10-17",
    "Id": "key-auto-policy-3",
    "Statement": [
        {
            "Sid": "iam-kms",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::$AWS_ACCOUNT_ID:root"
            },
            "Action": "kms:*",
            "Resource": "*"
        },
        {
            "Sid": "ec2-kms",
            "Effect": "Allow",
            "Principal": {
                "AWS": "*"
            },
            "Action": [
                "kms:Encrypt",
                "kms:Decrypt",
                "kms:ReEncrypt*",
                "kms:GenerateDataKey*",
                "kms:CreateGrant",
                "kms:DescribeKey"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "kms:CallerAccount": "$AWS_ACCOUNT_ID",
                    "kms:ViaService": "ec2.$AWS_REGION.amazonaws.com"
                }
            }
        }
    ]
}
EOF`

➤ Attach this policy document to the KMS key:

`aws kms put-key-policy --key-id $KEY_ID --policy file://key-policy.json`

➤ Finally, create a new storage class using the KMS key:

`cat >~/environment/ebs-kms-sc.yaml <<EOF
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: eks-auto-ebs-kms-sc
  annotations:
    storageclass.kubernetes.io/is-default-class: "true"
provisioner: ebs.csi.eks.amazonaws.com
volumeBindingMode: WaitForFirstConsumer
parameters:
  type: gp3
  encrypted: "true"
  kmsKeyId: $KEY_ID
EOF

kubectl apply -f ~/environment/ebs-kms-sc.yaml`

➤ Inspect the `StorageClass` you just created:

`kubectl describe storageclass eks-auto-ebs-kms-sc`

This should produce the following output:

`Name:            eks-auto-ebs-kms-sc
IsDefaultClass:  Yes
Annotations:     kubectl.kubernetes.io/last-applied-configuration={"apiVersion":"storage.k8s.io/v1","kind":"StorageClass","metadata":{"annotations":{"storageclass.kubernetes.io/is-default-class":"true"},"name":"eks-auto-ebs-kms-sc"},"parameters":{"encrypted":"true","kmsKeyId":"2d61cc69-7f98-474d-a663-b682872a9f6a","type":"gp3"},"provisioner":"ebs.csi.eks.amazonaws.com","volumeBindingMode":"WaitForFirstConsumer"}
,storageclass.kubernetes.io/is-default-class=true
Provisioner:           ebs.csi.eks.amazonaws.com
Parameters:            encrypted=true,kmsKeyId=2d61cc69-7f98-474d-a663-b682872a9f6a,type=gp3
AllowVolumeExpansion:  <unset>
MountOptions:          <none>
ReclaimPolicy:         Delete
VolumeBindingMode:     WaitForFirstConsumer
Events:                <none>`

We can make the following observations:

- `eks-auto-ebs-kms-sc` is configured as the default storage class.
- The associated provisioner is `ebs.csi.eks.amazonaws.com`. This provisioner is automatically made available by EKS Auto Mode.
- The EBS volume type is set to `gp3` (defaults to 3000 IOPS).
- The ReclaimPolicy is set to `Delete`, which means that when the associated PVC is deleted, this results in the deletion of both the PV object in Kubernetes, as well as the associated storage asset in the external infrastructure.
- The [VolumeBindingMode](https://kubernetes.io/docs/concepts/storage/storage-classes/#volume-binding-mode)  is set to `WaitForFirstConsumer`. This mode delays the binding and provisioning of a PersistentVolume until a pod using the PersistentVolumeClaim is created. PersistentVolumes will be selected or provisioned conforming to the topology that is specified by the pod's scheduling constraints. This is needed in situations where storage backends are topology-constrained and not globally accessible from all Nodes in the cluster (as would be the case where multiple AZs are used).
- Encryption is configured for volumes using the KMS key you created.

[**Update the `catalog` MySQL database pod**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/30-storage/20-storage-class#update-the-catalog-mysql-database-pod)

Now that we have a default `StorageClass` in place, let's update the `catalog` service to use it. Since many of StatefulSet fields, including volumeClaimTemplates, cannot be modified, we will uninstall the `catalog` component and then reinstall it, so we can update the volume type from emptyDir to a Persistent Volume.

➤ First, uninstall the current `catalog` service:

`helm uninstall retail-store-app-catalog`

Re-launch the `catalog` service using:

`helm upgrade -i retail-store-app-catalog oci://public.ecr.aws/aws-containers/retail-store-sample-catalog-chart --version ${RETAIL_STORE_APP_HELM_CHART_VERSION} -f - <<EOF
mysql:
  secret:
    create: true
    name: catalog-db
    username: catalog
    password: "mysqlcatalog123"
  persistentVolume:
    enabled: true
    accessMode:
      - ReadWriteOnce
    size: 30Gi
EOF`

## **Verify that the PVC for the catalog MySQL database has been created**

The re-launched `catalog` service should now have an associated `PersistentVolumeClaim`.

➤ You can see this by running:

`kubectl describe statefulset retail-store-app-catalog-mysql`

This time the output shows:

`Name:               retail-store-app-catalog-mysql
Namespace:          default
...
  Containers:
   mysql:
    Image:      public.ecr.aws/docker/library/mysql:8.0
    Port:       3306/TCP
    Host Port:  0/TCP
    Environment:
      MYSQL_ROOT_PASSWORD:  my-secret-pw
      MYSQL_DATABASE:       catalog
      MYSQL_USER:           <set to the key 'username' in secret 'catalog-db'>  Optional: false
      MYSQL_PASSWORD:       <set to the key 'password' in secret 'catalog-db'>  Optional: false
    Mounts:
      /var/lib/mysql from data (rw)
  Volumes:         <none>
  Node-Selectors:  <none>
  Tolerations:     <none>
Volume Claims:
  Name:          data
  StorageClass:
  Labels:        <none>
  Annotations:   <none>
  Capacity:      30Gi`

Let us inspect the PVC resource.

➤ To list all PVCs use:

`kubectl get pvc`

You should see:

`NAME                                    STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS          VOLUMEATTRIBUTESCLASS   AGE
data-retail-store-app-catalog-mysql-0   Bound    pvc-45a9e6ab-ed7c-47e1-9576-c3f01f33d327   30Gi       RWO            eks-auto-ebs-csi-sc   <unset>                 4h43m`

`data-retail-store-app-catalog-mysql-0` is the PVC created for the MySQL DB.

➤ Inspect it using:

`kubectl describe pvc data-retail-store-app-catalog-mysql-0`

This should produce the following output:

`Name:          data-retail-store-app-catalog-mysql-0
Namespace:     default
StorageClass:  eks-auto-ebs-kms-sc
Status:        Bound
Volume:        pvc-c5c4dec1-0ce5-4a00-982d-233c7d5bfdbb
Labels:        ...
Annotations:   pv.kubernetes.io/bind-completed: yes
               pv.kubernetes.io/bound-by-controller: yes
               volume.beta.kubernetes.io/storage-provisioner: ebs.csi.eks.amazonaws.com
               volume.kubernetes.io/selected-node: i-04a55c853d8acf24f
               volume.kubernetes.io/storage-provisioner: ebs.csi.eks.amazonaws.com
Finalizers:    [kubernetes.io/pvc-protection]
Capacity:      30Gi
Access Modes:  RWO
VolumeMode:    Filesystem
Used By:       retail-store-app-catalog-mysql-0
Events:        <none>`

From the output you can see that the PVC is bound to a specific PV (in this case `pvc-c5c4dec1-0ce5-4a00-982d-233c7d5bfdbb`), and that this has been provisioned using `ebs.csi.eks.amazonaws.com` with a capacity of 30Gi as specified in `values-catalog.yaml`.

➤ You can also inspect the PV as follows:

`kubectl describe pv $(kubectl get pvc data-retail-store-app-catalog-mysql-0 -o jsonpath="{.spec.volumeName}")`

The output should be similar to the below:

`Name:              pvc-c5c4dec1-0ce5-4a00-982d-233c7d5bfdbb
Labels:            <none>
Annotations:       pv.kubernetes.io/provisioned-by: ebs.csi.eks.amazonaws.com
                   volume.kubernetes.io/provisioner-deletion-secret-name:
                   volume.kubernetes.io/provisioner-deletion-secret-namespace:
Finalizers:        [external-provisioner.volume.kubernetes.io/finalizer kubernetes.io/pv-protection external-attacher/ebs-csi-eks-amazonaws-com]
StorageClass:      eks-auto-ebs-kms-sc
Status:            Bound
Claim:             default/data-retail-store-app-catalog-mysql-0
Reclaim Policy:    Delete
Access Modes:      RWO
VolumeMode:        Filesystem
Capacity:          30Gi
Node Affinity:
  Required Terms:
    Term 0:        topology.kubernetes.io/zone in [us-west-2a]
Message:
Source:
    Type:              CSI (a Container Storage Interface (CSI) volume source)
    Driver:            ebs.csi.eks.amazonaws.com
    FSType:            ext4
    VolumeHandle:      vol-05938b7ff13ef8ebf
    ReadOnly:          false
    VolumeAttributes:      storage.kubernetes.io/csiProvisionerIdentity=1735365022188-8218-ebs.csi.eks.amazonaws.com
Events:                <none>`

The `VolumeHandle` references the Amazon EBS Volume ID associated with the PV. Let's use this to inspect the EBS volume and check that it has been created correctly.

[**Verify that the EBS volume for the `catalog` MySQL database has been created correctly**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/30-storage/20-storage-class#verify-that-the-ebs-volume-for-the-catalog-mysql-database-has-been-created-correctly)

➤ Obtain the underlying Amazon EBS Volume ID as follows:

`MYSQL_PV_NAME=$(kubectl get pvc data-retail-store-app-catalog-mysql-0 -o jsonpath="{.spec.volumeName}")
MYSQL_EBS_VOL_ID=$(kubectl get pv $MYSQL_PV_NAME -o jsonpath="{.spec.csi.volumeHandle}")
echo EBS Volume ID: $MYSQL_EBS_VOL_ID`

➤ Display the details for the EBS volume:

`aws ec2 describe-volumes --volume-ids $MYSQL_EBS_VOL_ID --query Volumes[0]`

Note the following section of the output, proving that KMS encryption is enabled with the correct key:

    `...
    "Encrypted": true,
    "KmsKeyId": "arn:aws:kms:us-west-2:845041152230:key/2d61cc69-7f98-474d-a663-b682872a9f6a",
    ...
    "Iops": 3000,
    ...`

Note also that the `Iops` attribute is set to the gp3 default of 3000.

---

## **Summary**

In this section, you performed the following steps:

- Created a KMS key.
- Attached a key policy that enables EC2 instances in the account to use the KMS key for encrypting EBS volumes.
- Created a default `StorageClass` configured to use this key for encryption, and using a standard `gp3` volume.
- Updated the configuration of the `catalog` service to use the default `StorageClass` for creating a persistent volume.
- Verified that the EBS volume was created correctly, using the correct KMS key and also the default IOPS setting for gp3 volumes.

In the next section you will add a second `StorageClass` which provisions higher IOPS for gp3 volumes, and explicitly configures the `orders` PostgreSQL database to use this.

# Multiple EBS Storage Classes

[Overview](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/30-storage/30-multiiple-storage-classes#overview) | [Update StatefulSet configuration](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/30-storage/30-multiiple-storage-classes#update-statefulset) | [Summary](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/30-storage/30-multiiple-storage-classes#summary)

## **Overview**

In the previous section you created a default StorageClass and then configured the `catalog` service to use this to create a PV for its MySQL database.

The default StorageClass you created uses a KMS key to encrypt volumes, and also uses the default gp3 setting for IOPS (which you verified to be 3000).

Now suppose you were expecting a higher volume of traffic on the `orders` database, and needed to increase the IOPS accordingly.

In this section, you will create a second StorageClass that provisions an encrypted gp3 volume with 6000 IOPS, and then explicitly configure the `orders` PostgreSQL `StatefulSet` to use a PV based on this StorageClass.

## **Update StatefulSet configuration**

[**Create a second StorageClass with 6000 IOPS**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/30-storage/30-multiiple-storage-classes#create-a-second-storageclass-with-6000-iops)

➤ Create a StorageClass using the same KMS key from the previous section, but also specifying an IOPS value:

`cat >~/environment/ebs-iops-kms-sc.yaml <<EOF
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: eks-auto-ebs-iops-kms-sc
provisioner: ebs.csi.eks.amazonaws.com
volumeBindingMode: WaitForFirstConsumer
parameters:
  type: gp3
  iops: "6000"
  encrypted: "true"
  kmsKeyId: $KEY_ID
EOF

kubectl apply -f ~/environment/ebs-iops-kms-sc.yaml`

Note that this time we did not include an annotation to make this the default StorageClass. This means you will need to reference this StorageClass explicitly in order to use it.

[**Update the `orders` PostgreSQL database pod**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/30-storage/30-multiiple-storage-classes#update-the-orders-postgresql-database-pod)

Since we can't update some of the StatefulSet fields such as the `persistentVolumeClaimRetentionPolicy`, we will first have to uninstall the current version of the `orders` service, and reinstall it again.

➤ Execute the following command:

`helm uninstall retail-store-app-orders`

➤ Create a `values-orders.yaml` as follows:

`helm upgrade -i retail-store-app-orders oci://public.ecr.aws/aws-containers/retail-store-sample-orders-chart \
  --version ${RETAIL_STORE_APP_HELM_CHART_VERSION} -f - <<EOF
postgresql:
  secret:
    create: true
    name: orders-db
    username: orders
    password: "postgres123"
  persistentVolume:
    enabled: true
    accessMode:
      - ReadWriteOnce
    size: 20Gi
    storageClass: eks-auto-ebs-iops-kms-sc
EOF`

➤ Wait until the `orders` service is up and running again:

`kubectl wait --for=condition=Ready pod -l app.kubernetes.io/instance=retail-store-app-orders --namespace default --timeout=300s`

[**Verify that the PVC for the `orders` PostgreSQL database has been created**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/30-storage/30-multiiple-storage-classes#verify-that-the-pvc-for-the-orders-postgresql-database-has-been-created)

➤ List all PVCs:

`kubectl get pvc`

You should see:

`NAME                                        STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS               VOLUMEATTRIBUTESCLASS   AGE
data-retail-store-app-catalog-mysql-0       Bound    pvc-c5c4dec1-0ce5-4a00-982d-233c7d5bfdbb   30Gi       RWO            eks-auto-ebs-kms-sc        <unset>                 93m
data-retail-store-app-orders-postgresql-0   Bound    pvc-b1e886af-a019-4d98-adb0-d321e5dcab80   20Gi       RWO            eks-auto-ebs-iops-kms-sc   <unset>                 6m55s`

`data-retail-store-app-orders-postgresql-0` is the PVC created for the PostgreSQL DB.

➤ Inspect it using:

`kubectl describe pvc data-retail-store-app-orders-postgresql-0`

➤ You can also inspect the PV as follows:

`kubectl describe pv $(kubectl get pvc data-retail-store-app-orders-postgresql-0 -o jsonpath="{.spec.volumeName}")`

[**Verify that the EBS volume for the `orders` PostgreSQL database has been created correctly**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/30-storage/30-multiiple-storage-classes#verify-that-the-ebs-volume-for-the-orders-postgresql-database-has-been-created-correctly)

Let us verify that the IOPS attribute has been set correctly.

➤ Obtain the underlying AWS EBS Volume ID as follows:

`PGSQL_PV_NAME=$(kubectl get pvc data-retail-store-app-orders-postgresql-0 -o jsonpath="{.spec.volumeName}")
PGSQL_EBS_VOL_ID=$(kubectl get pv $PGSQL_PV_NAME -o jsonpath="{.spec.csi.volumeHandle}")
echo EBS Volume ID: $PGSQL_EBS_VOL_ID`

➤ Display the details for the EBS volume:

`aws ec2 describe-volumes --volume-ids $PGSQL_EBS_VOL_ID --query Volumes[0]`

Note the following sections of the output, proving that IOPS is set to 6000 and KMS encryption is enabled with the correct key:

    `...
    "Encrypted": true,
    "KmsKeyId": "arn:aws:kms:us-west-2:845041152230:key/2d61cc69-7f98-474d-a663-b682872a9f6a",
    "Size": 20,
    ...
    "Iops": 6000,
    ...`

---

## **Summary**

In this section, you performed the following steps:

- Created a StorageClass configured to use a KMS key for encryption, and using a standard `gp3` volume with 6000 provisioned IOPS.
- Updated the configuration of the `orders` service to use this new StorageClass for creating a persistent volume.
- Verified that the EBS volume was created correctly, using the correct KMS key and also the specified provisioned IOPS setting.

# Module 3 - Cluster Upgrades

## **Understanding Kubernetes upgrades in EKS**

Amazon Elastic Kubernetes Service (EKS) requires careful planning for upgrades. The upstream Kubernetes project ([Kubernetes Releases](https://kubernetes.io/releases/) ) undergoes continuous improvement, with regular updates introducing new functionalities, design enhancements, and bug corrections. Minor version releases typically occur every four months, and each version receives a community support for approximately [1 year](https://kubernetes.io/releases/patch-releases/#support-period)  following its launch.

## **Why keep EKS updated?**

Maintaining current Amazon EKS versions is crucial for:

1. **Security**: Protecting your Kubernetes clusters against vulnerabilities
2. **Stability**: Ensuring reliable performance and compatibility
3. **Innovation**: Accessing the latest platform features and capabilities

For detailed information about EKS versions and updates, refer to the [Amazon EKS Kubernetes versions documentation](https://docs.aws.amazon.com/eks/latest/userguide/kubernetes-versions.html) .

## **EKS Auto Mode: enhanced shared responsibility**

A Kubernetes deployment consists of both **control plane** and **data plane** components (worker nodes).

Amazon EKS has always managed the Kubernetes control plane and upgrades. Before Amazon EKS Auto Mode, cluster owners were responsible for initiating upgrades for both the control plane and data plane. This includes upgrading worker nodes in Self Managed node groups, Managed Node Groups, and other add-ons.

Amazon EKS Auto Mode represents a significant advancement in Kubernetes cluster management, expanding AWS's responsibility to include the automatic upgrading of cluster infrastructure. This enhancement covers both worker nodes and core cluster capabilities, substantially reducing the operational burden on customers.

To illustrate the shared responsibility model under Amazon EKS Auto Mode, please refer to the image below:

![](https://static.us-east-1.prod.workshops.aws/7c3be994-d644-4401-a817-8cd56d557506/static/images/cluster_upgrade/shared-responsibility-model-with-eks-auto.png?Key-Pair-Id=K36Q2WVO3JP7QD&Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9zdGF0aWMudXMtZWFzdC0xLnByb2Qud29ya3Nob3BzLmF3cy83YzNiZTk5NC1kNjQ0LTQ0MDEtYTgxNy04Y2Q1NmQ1NTc1MDYvKiIsIkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTc0OTA3NDM0NH19fV19&Signature=W6WTuafMUQvUflH%7EEhZzuRyjNJftCEdrCF0ejl38MozYLykI2mAetYKbF86h0RLLnGofroTZPhK4yllzqxsaaDSSyRgze9Fvpjk0Ms1L8UBqAyv4jFwndJaf%7E4fBxBzS2cHu3Rk0lLG4Xo5Cb8A9PVDycYG8E%7Ez0HoIo2kyXPShI1JRocSpKKGDl50WVnd%7EQ8pQrxUD3L-ENWiyWP3JiuvViPXvc8mUUlCiCY0u9Jk%7E0LFiQm68sCn44JqL07uXLX3MpmBTchq-uqZdXWv1w5pouYAg-w9wgD5az4UBmySpxyRIPWFycxq4Gdy08r-AkurESWkXfjl3Bh%7EDkAPvLDg__)

[**Component Management**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/30-cluster-upgrades#component-management)

- **Red areas**: represent components fully managed by AWS
- **Green areas**: indicate the aspects that remain under customer management

## **Kubernetes Version Structure**

From the [Kubernetes versioning documentation](https://kubernetes.io/releases/) : Versions are expressed as **x.y.z**, where:

- **x**: Major version
- **y**: Minor version (Released every ~4 months)
- **z**: Patch version (Monthly releases)

The Kubernetes version indicates both control-plane (apiserver, controller-manager, etc.) and data-plane (e.g., kubelet, kube-proxy, etc.) components.

## **Amazon EKS Version Management**

Amazon EKS provides a managed Kubernetes control plane with a range of [supported versions](https://docs.aws.amazon.com/eks/latest/userguide/kubernetes-versions.html#kubernetes-release-calendar) :

- **Standard Support**: 14 months
- **Extended Support**: Additional 12 months (optional with additional costs, which can be [disabled](https://docs.aws.amazon.com/eks/latest/userguide/disable-extended-support.html) )
- **Version Compatibility**: Data-plane components (e.g., kubelet, kube-proxy) should match the control plane minor version but can also stay on lower versions up to the allowed [version skew policy](https://kubernetes.io/releases/version-skew-policy/) . When using node auto-scalers such as Karpenter, the AMI minor version can be automatically discovered to match the EKS Control plane version.

## **Amazon EKS platform versions - Kubernetes control-plane patch versions upgrade**

Amazon EKS periodically releases new [platform versions](https://docs.aws.amazon.com/eks/latest/userguide/platform-versions.html)  to enable new control plane settings and provide security fixes. Each Kubernetes minor version may have multiple associated platform versions. These EKS Platform versions are automatically upgraded in a gradual rollout process with no manual intervention from the customer side. Lastly, new Amazon EKS platform versions don’t introduce breaking changes or cause service interruptions. Staying current with the latest Kubernetes minor version is crucial for maintaining a secure and efficient EKS environment. This approach aligns with the shared responsibility model in Amazon EKS, ensuring that clusters run with the latest security patches and bug fixes, thereby reducing security vulnerabilities. Additionally, it offers improved performance, scalability, and reliability, ultimately providing better service to applications and customers.

[**Example**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/30-cluster-upgrades#example)

If your cluster runs Kubernetes 1.25, AWS might update your platform version from **eks.1** to **eks.2** automatically to apply security patches while maintaining the same Kubernetes version.

## **Add-ons Management**

The last part of an upgrade process is to upgrade the [add-ons](https://kubernetes.io/docs/concepts/cluster-administration/addons/)  which are system wide applications that provides additional capabilities for other business applications that run on the cluster For example:

- Observability tools
- Security implementations
- Networking solutions
- Storage integrations

Amazon EKS provides additional guidance on upgrades as part of the EKS best practices guide which you can find in the following [link](https://docs.aws.amazon.com/eks/latest/best-practices/cluster-upgrades.html)

After understanding the Kubernetes version cadence and compatibility, next you're going to experiment with how Amazon EKS Auto Mode manages zero touch upgrades of cluster infrastructure that includes nodes and the core capabilities.

# Understanding upgrades with Amazon EKS Auto Mode

[Overview](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/30-cluster-upgrades/10-understanding-upgrades#overview) | [Upgrade flow process](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/30-cluster-upgrades/10-understanding-upgrades#upgrade) | [Time controls](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/30-cluster-upgrades/10-understanding-upgrades#time-controls) | [Summary](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/30-cluster-upgrades/10-understanding-upgrades#summary)

---

## **Overview**

![](https://static.us-east-1.prod.workshops.aws/7c3be994-d644-4401-a817-8cd56d557506/static/images/cluster_upgrade/upgrade_flow.png?Key-Pair-Id=K36Q2WVO3JP7QD&Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9zdGF0aWMudXMtZWFzdC0xLnByb2Qud29ya3Nob3BzLmF3cy83YzNiZTk5NC1kNjQ0LTQ0MDEtYTgxNy04Y2Q1NmQ1NTc1MDYvKiIsIkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTc0OTA3NDM0NH19fV19&Signature=W6WTuafMUQvUflH%7EEhZzuRyjNJftCEdrCF0ejl38MozYLykI2mAetYKbF86h0RLLnGofroTZPhK4yllzqxsaaDSSyRgze9Fvpjk0Ms1L8UBqAyv4jFwndJaf%7E4fBxBzS2cHu3Rk0lLG4Xo5Cb8A9PVDycYG8E%7Ez0HoIo2kyXPShI1JRocSpKKGDl50WVnd%7EQ8pQrxUD3L-ENWiyWP3JiuvViPXvc8mUUlCiCY0u9Jk%7E0LFiQm68sCn44JqL07uXLX3MpmBTchq-uqZdXWv1w5pouYAg-w9wgD5az4UBmySpxyRIPWFycxq4Gdy08r-AkurESWkXfjl3Bh%7EDkAPvLDg__)

Amazon EKS Auto Mode revolutionizes Kubernetes cluster management by providing zero-touch updates for your entire cluster infrastructure.

## **Upgrade flow process**

[**1. Version Verification**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/30-cluster-upgrades/10-understanding-upgrades#1.-version-verification)

- The cluster owner checks the latest available Amazon EKS version and verify compatibility with current applications
- The cluster owner can initiate a version update

[**2. Control Plane and cluster component updates**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/30-cluster-upgrades/10-understanding-upgrades#2.-control-plane-and-cluster-component-updates)

- Initiate control plane version upgrade
- With Auto Mode, any of the managed cluster capabilities will also be automatically updated to ensure compatibility across versions

[**3. Data Plane Update**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/30-cluster-upgrades/10-understanding-upgrades#3.-data-plane-update)

![](https://static.us-east-1.prod.workshops.aws/7c3be994-d644-4401-a817-8cd56d557506/static/images/cluster_upgrade/node_rolling_upgrade.png?Key-Pair-Id=K36Q2WVO3JP7QD&Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9zdGF0aWMudXMtZWFzdC0xLnByb2Qud29ya3Nob3BzLmF3cy83YzNiZTk5NC1kNjQ0LTQ0MDEtYTgxNy04Y2Q1NmQ1NTc1MDYvKiIsIkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTc0OTA3NDM0NH19fV19&Signature=W6WTuafMUQvUflH%7EEhZzuRyjNJftCEdrCF0ejl38MozYLykI2mAetYKbF86h0RLLnGofroTZPhK4yllzqxsaaDSSyRgze9Fvpjk0Ms1L8UBqAyv4jFwndJaf%7E4fBxBzS2cHu3Rk0lLG4Xo5Cb8A9PVDycYG8E%7Ez0HoIo2kyXPShI1JRocSpKKGDl50WVnd%7EQ8pQrxUD3L-ENWiyWP3JiuvViPXvc8mUUlCiCY0u9Jk%7E0LFiQm68sCn44JqL07uXLX3MpmBTchq-uqZdXWv1w5pouYAg-w9wgD5az4UBmySpxyRIPWFycxq4Gdy08r-AkurESWkXfjl3Bh%7EDkAPvLDg__)

Graceful node updates following:

- Node replacement with latest AMIs by using Drift management from Karpenter capability
- Rolling update strategy
- Respect Pod Disruption Budgets (PDBs)

## **Time controls**

[**Expiration Settings**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/30-cluster-upgrades/10-understanding-upgrades#expiration-settings)

- Default: the worker nodes will be fully automatically upgraded no later than **14** days
- Custom NodePools: Up to **21** days

[**Termination Grace Period**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/30-cluster-upgrades/10-understanding-upgrades#termination-grace-period)

Amazon EKS Auto Mode sets a default of 24 hrs for terminationGracePeriod. The terminationGracePeriod defines the amount of time a Node can be drained before Karpenter forcibly cleans up the node. Pods blocking eviction like PDBs and do-not-disrupt will be respected during draining until the terminationGracePeriod is reached, where those pods will be forcibly deleted.

[**Disruption Controls**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/30-cluster-upgrades/10-understanding-upgrades#disruption-controls)

We can limit the rate of how Amazon EKS Auto Mode disrupt nodes through the NodePool's `spec.disruption.budgets`. With disruption budgets we can control the rate of worker nodes upgrades or making sure upgrades only happens during specific dates and times (using schedule).

Disruption budgets can be configured for the following disruption reasons:

- Empty - when a node is Empty
- Underutilized - a node is Underutilized as can be removed or replaced with another small sized node
- Drifted - when a node is marked as Drifted from its desired state (e.g. EKS control plane version differs from worker node version)

By default, Amazon EKS Auto Mode general-purpose NodePool has the following disruption budgets.

`...
spec:
  disruption:
    consolidateAfter: 0s
    consolidationPolicy: WhenEmptyOrUnderutilized
    budgets:
    - nodes: 10%
...`

With this budget, Amazon EKS Auto Mode will disrupt at most 10% of active nodes at a time.

`...
spec:
  disruption:
    consolidateAfter: 0s
    consolidationPolicy: WhenEmptyOrUnderutilized
    budgets:
    - nodes: 10%
    - schedule: 0 9 * * mon-fri
      duration: 8h
      nodes: "0"
      reasons:
      - Drifted
...`

With this budget, we limit Amazon EKS Auto Mode to not disrupt nodes ("0") during the weekdays business hours if Drift is triggered, and allow only at most 10% of active nodes to be disrupted at all other times.

---

## **Summary**

Now that we have this background, let's go on to upgrading the cluster to the most recent Kubernetes version.

# Upgrading the cluster

[Upgrade](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/30-cluster-upgrades/20-upgrades#upgrade) | [Summary](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/30-cluster-upgrades/20-upgrades#summary)

---

## **Upgrade the cluster**

In this section of the workshop, you will gain hands-on experience with Amazon EKS Auto Mode's automatic cluster infrastructure updates. You'll begin by updating the control plane.

[**Check Current Versions**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/30-cluster-upgrades/20-upgrades#check-current-versions)

➤ First, let's check the current Amazon EKS control plane version:

`aws eks describe-cluster --region $AWS_REGION --name $DEMO_CLUSTER_NAME --query "cluster.version" --output text`

This is the output:

`1.30`

We can see that our Amazon EKS control plane is running Amazon EKS version *1.30*.

➤ Now, let's observe the current worker nodes (data plane) version:

`kubectl get nodes`

The output should be similar to the following:

`NAME                  STATUS   ROLES    AGE     VERSION
i-0045ee24780784252   Ready    <none>   174m   v1.30.8-eks-3c20087
i-0471c7f38f676feda   Ready    <none>   173m   v1.30.8-eks-3c20087
i-084413db9a7008f06   Ready    <none>   174m   v1.30.8-eks-3c20087
...`

We can see that the worker node is also running Amazon EKS version *1.30*.

[**Look for deprecated APIs and new versions for additional components installed in the cluster**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/30-cluster-upgrades/20-upgrades#look-for-deprecated-apis-and-new-versions-for-additional-components-installed-in-the-cluster)

Under the shared responsibility model, you have to look into the [Kubernetes release](https://kubernetes.io/releases/)  page, and for each version you're upgrading to, verify that there are no API deprecations or changes that affect your business application.

Additionally, you have to look for new versions for any 3rd party or community addons you've installed in your cluster, and upgrade them post your EKS cluster upgrade.

[**Upgrade the control plane**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/30-cluster-upgrades/20-upgrades#upgrade-the-control-plane)

Let's upgrade our Amazon EKS control plane version to *1.31*.

**Note**: While there are multiple ways to upgrade an Amazon EKS control plane (using eksctl, AWS Console, AWS CLI, or Infrastructure as Code), we'll use the AWS CLI for simplicity in this workshop.

➤ Execute the following command:

`aws eks update-cluster-version --region $AWS_REGION --name $DEMO_CLUSTER_NAME --kubernetes-version 1.31`

You will see output similar to this:

`{
    "update": {
        "id": "c21285af-0500-34ea-9d97-aefad824508c",
        "status": "InProgress",
        "type": "VersionUpdate",
        "params": [
            {
                "type": "Version",
                "value": "1.31"
            },
            {
                "type": "PlatformVersion",
                "value": "eks.17"
            }
        ],
        "createdAt": "2025-01-07T16:34:37.094000+01:00",
        "errors": []
    }
}`

In the output, the Amazon EKS version is going to be updated to 1.31. Also pay attention to the `PlatformVersion` parameters which is documented in the [Amazon EKS platform version](https://docs.aws.amazon.com/eks/latest/userguide/platform-versions.html) . Note that at the time of the creation of this workshop, this output is *eks.17*, but can be different in future platform versions of Amazon EKS.

**Note**

The control plane upgrade process typically takes about 10 minutes. Depending on your available time, we advise you to either take a small break here, or progress to the [Migration patterns module](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/40-migrations), and get back to [check the upgrade](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/30-cluster-upgrades/30-check-the-upgrade.md) once you're done.

---

## **Summary**

In this section we've upgraded the Amazon EKS Auto Mode cluster control plane.

### [Amazon EKS Masterclass: Advanced Live Learning Session](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/30-cluster-upgrades/30-check-the-upgrade#:~:text=Checking%20the%20upgrade-,Checking%20the%20upgrade,Previous,-Next)

Checking the upgrade
Check the upgrade | Summary

Check the upgrade
Note that upgrading the cluster may take several minutes.

➤ Using the aws eks-describe-cluster aws cli command, we will check if the upgrade process is complete, and our cluster version is 1.31. If it's not, please allow some more time for the upgrade process to complete.

aws eks describe-cluster --region $AWS_REGION --name $DEMO_CLUSTER_NAME --query "cluster.version" --output text

1.31
The control plane is now running Amazon EKS version 1.31.

➤ Verify the nodes:

kubectl get nodes

NAME                  STATUS   ROLES    AGE     VERSION
i-0ffd20214100093ac   Ready    <none>   14m     v1.31.5-eks-baa6d11
The worker node is also running Amazon EKS version 1.31.

We can see that there are events related to Drifted/Replaced, those were triggered because Amazon EKS Auto Mode detected that the EKS control plane version differs from worker node version and triggered a replacement via Drift.

➤ Execute the following command:

kubectl get events | grep Drifted/Replace

7m28s       Normal    DisruptionLaunching              nodeclaim/general-purpose-557w8        Launching NodeClaim: Drifted/Replace
6m53s       Normal    DisruptionTerminating            nodeclaim/general-purpose-k4kxp        Disrupting NodeClaim: Drifted/Replace
6m53s       Normal    DisruptionTerminating            node/i-0ffd20214100093ac               Disrupting Node: Drifted/Replace
Amazon EKS Auto Mode will first launch a new node replacement, evict Pods, and then wait until the new node replacement is Ready before terminating the node to be replaced. When PDBs are configured, Auto Mode respects PDBs by using a backoff retry eviction strategy. Pods will never be forcibly deleted, so pods that fail to shut down will prevent a node from deleting and will forcefully be deleted when the terminationGracePeriod is reached.

Summary
Congratulations! In this section you have successfully updated your cluster to the latest version of Kubernetes.

## Module 4 - Migrate an Amazon EKS Cluster to EKS Auto Mode

In this module we will explore migration strategies from an existing Amazon EKS cluster to EKS Auto Mode.

We will use an existing Amazon EKS cluster with several different compute options for the worker nodes which host the cluster's applications and operational software and gradually migrate from each one of these options to Amazon EKS Auto Mode.

Table of Contents
Cluster configuration
Enabling EKS Auto Mode
Migrating from AWS Fargate
Migrating from EKS Managed Node Groups
Migrating from a Self-Managed Karpenter
Migrating Networking Resources
Removing non-EKS Auto Mode Add-ons and Compute

# Cluster configuration

[Setup](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/40-migrations/10-cluster-configuration#setup) | [Overview](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/40-migrations/10-cluster-configuration#overview) | [Cluster Add-ons](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/40-migrations/10-cluster-configuration#addons) | [Self-Managed Karpenter Configuration](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/40-migrations/10-cluster-configuration#self-managed-karpenter-config) | [Demo Application](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/40-migrations/10-cluster-configuration#demo-application)

---

## **Setup**

During the provision of this workshop we've created several Amazon EKS clusters, with one specifically intended for this module.

➤ Before we begin, switch the current `kubeconfig` context by executing:

`kubectl config use-context arn:aws:eks:${AWS_REGION}:${AWS_ACCOUNT_ID}:cluster/${MIGRATION_CLUSTER_NAME}`

You should receive an output similar to:

`Switched to context "<a cluster ARN>".`

➤ Verify the cluster setup by executing the following command:

`kubectl get nodes -o json | jq -r '.items[].metadata.labels | ."kubernetes.io/hostname" + " | " + ."topology.kubernetes.io/zone" + " | " + (."eks.amazonaws.com/capacityType" // if ."eks.amazonaws.com/compute-type" == "fargate" then "FARGATE" else "KARPENTER" end) + " | " + (."eks.amazonaws.com/nodegroup" // if ."karpenter.sh/nodepool" then "nodepool: " + ."karpenter.sh/nodepool" else "profile: apps" end)' | column -t | sort -k 5`

The command above shows the distribution of compute instances in the cluster across compute options and should look similar to the following:

`fargate-ip-192-168-116-56.us-west-2.compute.internal   |  us-west-2c  |  FARGATE    |  profile:    apps
fargate-ip-192-168-180-168.us-west-2.compute.internal  |  us-west-2b  |  FARGATE    |  profile:    apps
fargate-ip-192-168-191-115.us-west-2.compute.internal  |  us-west-2b  |  FARGATE    |  profile:    apps
ip-192-168-100-194.us-west-2.compute.internal          |  us-west-2c  |  KARPENTER  |  nodepool:   apps
ip-192-168-155-246.us-west-2.compute.internal          |  us-west-2a  |  KARPENTER  |  nodepool:   apps
...
ip-192-168-173-151.us-west-2.compute.internal          |  us-west-2b  |  KARPENTER  |  nodepool:   apps
ip-192-168-28-67.us-west-2.compute.internal            |  us-west-2c  |  ON_DEMAND  |  apps-mng
ip-192-168-51-140.us-west-2.compute.internal           |  us-west-2a  |  ON_DEMAND  |  apps-mng
ip-192-168-83-58.us-west-2.compute.internal            |  us-west-2b  |  ON_DEMAND  |  apps-mng
ip-192-168-26-158.us-west-2.compute.internal           |  us-west-2c  |  ON_DEMAND  |  system-mng  
ip-192-168-33-46.us-west-2.compute.internal            |  us-west-2a  |  ON_DEMAND  |  system-mng  
ip-192-168-86-255.us-west-2.compute.internal           |  us-west-2b  |  ON_DEMAND  |  system-mng`

Note that self-managed Karpenter nodes distribution may differ due to the dynamic nature of Karpenter provision and consolidation (hence `...` in the output above), but the nodes should follow the same approximate distribution.

## **Overview**

The compute options in the cluster, as shown in the output above, include:

- An AWS Fargate [profile](https://docs.aws.amazon.com/eks/latest/userguide/fargate-profile.html)  that allows to target specific applications to be scheduled on [AWS Fargate](https://aws.amazon.com/fargate/) . These are the lines marked by `profile: apps`.
- Several [Amazon EKS managed node group](https://docs.aws.amazon.com/eks/latest/userguide/managed-node-groups.html)  that host the cluster operational software and some of the applications. These are the lines marked by `system-mng` for the cluster-critical managed node group and `apps-mng` for the applications' managed node group.
- A self-managed [Karpenter](https://karpenter.sh/)  nodes that host the rest of the applications in the cluster. These are marked by `nodepool: apps`.

The cluster will also contain the required [Amazon EKS add-ons](https://docs.aws.amazon.com/eks/latest/userguide/eks-add-ons.html) :

- the [Amazon VPC CNI plugin for Kubernetes](https://docs.aws.amazon.com/eks/latest/userguide/workloads-add-ons-available-eks.html#add-ons-vpc-cni)  add-on, which provides native VPC networking for the cluster
- the [CoreDNS](https://docs.aws.amazon.com/eks/latest/userguide/workloads-add-ons-available-eks.html#add-ons-coredns)  add-on, which serves as the Kubernetes cluster DNS server
- the [Kube-proxy](https://docs.aws.amazon.com/eks/latest/userguide/workloads-add-ons-available-eks.html#add-ons-kube-proxy)  add-on, which maintains network rules on each Amazon EC2 worker node
- the [EKS Pod Identity Agent](https://docs.aws.amazon.com/eks/latest/userguide/workloads-add-ons-available-eks.html#add-ons-pod-id)  add-on, which manages AWS credentials for the cluster applications

In addition, the cluster will also include a self-managed [AWS Load Balancer Controller](https://kubernetes-sigs.github.io/aws-load-balancer-controller/latest/) , that provisions and configures Elastic Load Balancers ([Network Load Balancers](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/introduction.html)  for Service resources and [Application Load Balancers](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html)  for Ingress resources), to expose the cluster applications to traffic.

➤ You can validate that all the applications and controllers are operational (in a `Running` state) by executing:

`kubectl get pods -A`

Note that due to the provision process, some Pods may have a non-zero `RESTARTS` count. As long as these aren't recent (dozens of minutes ago), your cluster is in the desired state.

## **Cluster Add-ons**

The cluster add-ons we’ve mentioned above are either DaemonSets (VPC CNI, kube-proxy and Pod Identity agent) or Deployments (CoreDNS, Karpenter and Application Load Balancer Controller) and thus their required compute capacity is handled differently.

The DaemonSets will be deployed on every worker node in the cluster, while the rest will be deployed on a specifically configured system-mng managed node group.

The `system-mng` node group is provisioned along with the cluster and its configuration can be represented, for reference, by the following CloudFormation snippet:

`1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
...
  SystemNodegroup:
    Type: AWS::EKS::Nodegroup
    Properties:
      NodegroupName: system-mng
      ...
      AmiType: AL2023_ARM_64_STANDARD
      NodeRole: !GetAtt NodeRole.Arn
      InstanceTypes:
        - t4g.small
      ScalingConfig:
        MinSize: 0
        DesiredSize: 3
        MaxSize: 3
      Labels:
        role: system-mng
      Taints:
        - Key: role
          Value: system-mng
          Effect: NO_SCHEDULE
      Subnets:
        ...
...`

Note the `role=system` label and the `role=system` taint in the configuration of the managed node group. These are set to ensure that only the selected software/applications can be scheduled onto this node group's instances.

The relevant add-ons then define a matching toleration and target the node group above using a matching node selector.

➤ You can view the node group and its configuration in the [AWS EKS console](https://console.aws.amazon.com/eks/home#/clusters)  and navigating to the workshop **migration** cluster, which should look like this:

![](https://static.us-east-1.prod.workshops.aws/7c3be994-d644-4401-a817-8cd56d557506/static/images/migration/system-mng.png?Key-Pair-Id=K36Q2WVO3JP7QD&Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9zdGF0aWMudXMtZWFzdC0xLnByb2Qud29ya3Nob3BzLmF3cy83YzNiZTk5NC1kNjQ0LTQ0MDEtYTgxNy04Y2Q1NmQ1NTc1MDYvKiIsIkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTc0OTA3NDM0NH19fV19&Signature=W6WTuafMUQvUflH%7EEhZzuRyjNJftCEdrCF0ejl38MozYLykI2mAetYKbF86h0RLLnGofroTZPhK4yllzqxsaaDSSyRgze9Fvpjk0Ms1L8UBqAyv4jFwndJaf%7E4fBxBzS2cHu3Rk0lLG4Xo5Cb8A9PVDycYG8E%7Ez0HoIo2kyXPShI1JRocSpKKGDl50WVnd%7EQ8pQrxUD3L-ENWiyWP3JiuvViPXvc8mUUlCiCY0u9Jk%7E0LFiQm68sCn44JqL07uXLX3MpmBTchq-uqZdXWv1w5pouYAg-w9wgD5az4UBmySpxyRIPWFycxq4Gdy08r-AkurESWkXfjl3Bh%7EDkAPvLDg__)

![](https://static.us-east-1.prod.workshops.aws/7c3be994-d644-4401-a817-8cd56d557506/static/images/migration/system-mng-labels.png?Key-Pair-Id=K36Q2WVO3JP7QD&Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9zdGF0aWMudXMtZWFzdC0xLnByb2Qud29ya3Nob3BzLmF3cy83YzNiZTk5NC1kNjQ0LTQ0MDEtYTgxNy04Y2Q1NmQ1NTc1MDYvKiIsIkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTc0OTA3NDM0NH19fV19&Signature=W6WTuafMUQvUflH%7EEhZzuRyjNJftCEdrCF0ejl38MozYLykI2mAetYKbF86h0RLLnGofroTZPhK4yllzqxsaaDSSyRgze9Fvpjk0Ms1L8UBqAyv4jFwndJaf%7E4fBxBzS2cHu3Rk0lLG4Xo5Cb8A9PVDycYG8E%7Ez0HoIo2kyXPShI1JRocSpKKGDl50WVnd%7EQ8pQrxUD3L-ENWiyWP3JiuvViPXvc8mUUlCiCY0u9Jk%7E0LFiQm68sCn44JqL07uXLX3MpmBTchq-uqZdXWv1w5pouYAg-w9wgD5az4UBmySpxyRIPWFycxq4Gdy08r-AkurESWkXfjl3Bh%7EDkAPvLDg__)

![](https://static.us-east-1.prod.workshops.aws/7c3be994-d644-4401-a817-8cd56d557506/static/images/migration/system-mng-taints.png?Key-Pair-Id=K36Q2WVO3JP7QD&Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9zdGF0aWMudXMtZWFzdC0xLnByb2Qud29ya3Nob3BzLmF3cy83YzNiZTk5NC1kNjQ0LTQ0MDEtYTgxNy04Y2Q1NmQ1NTc1MDYvKiIsIkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTc0OTA3NDM0NH19fV19&Signature=W6WTuafMUQvUflH%7EEhZzuRyjNJftCEdrCF0ejl38MozYLykI2mAetYKbF86h0RLLnGofroTZPhK4yllzqxsaaDSSyRgze9Fvpjk0Ms1L8UBqAyv4jFwndJaf%7E4fBxBzS2cHu3Rk0lLG4Xo5Cb8A9PVDycYG8E%7Ez0HoIo2kyXPShI1JRocSpKKGDl50WVnd%7EQ8pQrxUD3L-ENWiyWP3JiuvViPXvc8mUUlCiCY0u9Jk%7E0LFiQm68sCn44JqL07uXLX3MpmBTchq-uqZdXWv1w5pouYAg-w9wgD5az4UBmySpxyRIPWFycxq4Gdy08r-AkurESWkXfjl3Bh%7EDkAPvLDg__)

➤ You can verify the relevant, non-DaemonSet add-ons deployment by executing the following command:

`export SYSTEM_NODES=$(kubectl get nodes -o json | jq -r '[.items[].metadata.labels | select(."eks.amazonaws.com/nodegroup" == "system-mng") | ."kubernetes.io/hostname"] | join("\\|")')
export DAEMONSETS_PODS=$(kubectl get ds -n kube-system -o json | jq -r '[.items[].metadata.name] | join ("\\|")')

kubectl get pods --all-namespaces -o wide | grep "${SYSTEM_NODES}" | grep -v "${DAEMONSETS_PODS}"`

The output should show at least CoreDNS, Karpenter, and Application Load Balancer Controller, similar to the following:

`kube-system   aws-load-balancer-controller-8c9657c99-c4hw4       1/1     Running   0             35m     192.168.41.16     ip-192-168-33-46.us-west-2.compute.internal             <none>           <none>
kube-system   aws-load-balancer-controller-8c9657c99-hhwdv       1/1     Running   0             35m     192.168.69.64     ip-192-168-86-255.us-west-2.compute.internal            <none>           <none>
kube-system   coredns-6d5c5bdb9f-2t2pw                           1/1     Running   0             45m     192.168.90.238    ip-192-168-86-255.us-west-2.compute.internal            <none>           <none>
kube-system   coredns-6d5c5bdb9f-7jswn                           1/1     Running   0             45m     192.168.94.40     ip-192-168-86-255.us-west-2.compute.internal            <none>           <none>
kube-system   karpenter-b677796f8-2n998                          1/1     Running   0             35m     192.168.31.184    ip-192-168-26-158.us-west-2.compute.internal            <none>           <none>
kube-system   karpenter-b677796f8-x5clj                          1/1     Running   0             35m     192.168.53.232    ip-192-168-33-46.us-west-2.compute.internal             <none>           <none>
kube-system   metrics-server-7d99f5f76c-6xz9f                    1/1     Running   0             45m     192.168.72.50     ip-192-168-86-255.us-west-2.compute.internal            <none>           <none>
kube-system   metrics-server-7d99f5f76c-zkpxg                    1/1     Running   0             45m     192.168.70.163    ip-192-168-86-255.us-west-2.compute.internal            <none>           <none>`

## **Self-Managed Karpenter Configuration**

To allow the self-managed Karpenter to provision instances for our applications’ Pods, we [need](https://karpenter.sh/docs/concepts/)  to define at least one NodeClass and one NodePool.

The configuration applied to the cluster can be represented, for reference, by the following partial snippet:

`EC2NodeClass`:

`1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
apiVersion: karpenter.k8s.aws/v1
kind: EC2NodeClass
metadata:
  name: apps
spec:
  amiSelectorTerms:
    - alias: al2023@latest
  role: KarpenterNodeRole-${MIGRATION_CLUSTER_NAME}
  subnetSelectorTerms:
    - tags:
        karpenter.sh/discovery: ${MIGRATION_CLUSTER_NAME}
        Name: "*/SubnetPrivate*"
  securityGroupSelectorTerms:
    - tags:
        karpenter.sh/discovery: ${MIGRATION_CLUSTER_NAME}`

`NodePool`:

`1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
  name: apps
spec:
  disruption:
    consolidationPolicy: WhenEmptyOrUnderutilized
    consolidateAfter: 30s
  template:
    metadata:
      labels:
        role: apps-karpenter
    spec:
      nodeClassRef:
        group: karpenter.k8s.aws
        kind: EC2NodeClass
        name: apps
      taints:
        - key: role
          value: apps-karpenter
          effect: NoSchedule
      requirements:
        - key: kubernetes.io/arch
          operator: In
          values: [amd64, arm64]
        - key: kubernetes.io/os
          operator: In
          values: [linux]
        - key: karpenter.sh/capacity-type
          operator: In
          values: [on-demand]
        - key: node.kubernetes.io/instance-category
          operator: In
          values: [c, m, r]
        - key: karpenter.k8s.aws/instance-generation
          operator: Gt
          values: ['4']
        - key: karpenter.k8s.aws/instance-size
          operator: NotIn
          values: [nano, micro, small, medium]`

Note the `role=apps-karpenter` label and the `role=apps-karpenter` taint in the configuration of the node pool above. These are set, in the same manner as the `system-mng` node group above, to ensure that only the selected applications can be scheduled using this Karpenter node pool.

## **Demo Application**

To demonstrate the migration process we will use the demo retail application – a sample application designed to illustrate container-related concepts on AWS.

➤ You can explore the application by executing the command below, Ctrl/Cmd-clicking the URL in the output, and adding a couple of items to the cart:

`kubectl get ingress -n apps retail-store-app-ui-main \
  -o jsonpath="http://{.status.loadBalancer.ingress[*].hostname}{'\n'}"`

The [application](https://github.com/aws-containers/retail-store-sample-app/tree/main)  contains several components in various languages and frameworks that use pre-built container images for both x86-64 and ARM64 CPU architectures:

![](https://static.us-east-1.prod.workshops.aws/7c3be994-d644-4401-a817-8cd56d557506/static/images/migration/application.png?Key-Pair-Id=K36Q2WVO3JP7QD&Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9zdGF0aWMudXMtZWFzdC0xLnByb2Qud29ya3Nob3BzLmF3cy83YzNiZTk5NC1kNjQ0LTQ0MDEtYTgxNy04Y2Q1NmQ1NTc1MDYvKiIsIkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTc0OTA3NDM0NH19fV19&Signature=W6WTuafMUQvUflH%7EEhZzuRyjNJftCEdrCF0ejl38MozYLykI2mAetYKbF86h0RLLnGofroTZPhK4yllzqxsaaDSSyRgze9Fvpjk0Ms1L8UBqAyv4jFwndJaf%7E4fBxBzS2cHu3Rk0lLG4Xo5Cb8A9PVDycYG8E%7Ez0HoIo2kyXPShI1JRocSpKKGDl50WVnd%7EQ8pQrxUD3L-ENWiyWP3JiuvViPXvc8mUUlCiCY0u9Jk%7E0LFiQm68sCn44JqL07uXLX3MpmBTchq-uqZdXWv1w5pouYAg-w9wgD5az4UBmySpxyRIPWFycxq4Gdy08r-AkurESWkXfjl3Bh%7EDkAPvLDg__)

The application components are deployed as follows:

| Component | Compute Option |
| --- | --- |
| **Assets** | Fargate |
|  |  |
| **Orders** | Managed Node Group |
| **Orders PostgreSQL database** | Managed Node Group |
| **Orders RabbitMQ** | Managed Node Group |
|  |  |
| **Catalog** | Managed Node Group |
| **Catalog MySQL database** | Managed Node Group |
|  |  |
| **Checkout** | Self-Managed Karpenter |
| **Checkout Redis in-memory database** | Self-Managed Karpenter |
|  |  |
| **Carts** | Self-Managed Karpenter |
| **Carts DynamoDB local database** | Self-Managed Karpenter |
|  |  |
| **UI** | Self-Managed Karpenter |

➤ Print out the distribution of instances across all capacity types by executing the following command:

`kubectl get nodes -o json | jq -r '.items[].metadata.labels | ."kubernetes.io/hostname" + " | " + ."topology.kubernetes.io/zone" + " | " + (."eks.amazonaws.com/capacityType" // if ."eks.amazonaws.com/compute-type" == "fargate" then "FARGATE" else "KARPENTER" end) + " | " + (."eks.amazonaws.com/nodegroup" // if ."karpenter.sh/nodepool" then "nodepool: " + ."karpenter.sh/nodepool" else "profile: apps" end)' | column -t | sort -k 5`

This should produce a result similar to the following:

`fargate-ip-192-168-116-56.us-west-2.compute.internal   |  us-west-2c  |  FARGATE    |  profile:    apps
fargate-ip-192-168-180-168.us-west-2.compute.internal  |  us-west-2b  |  FARGATE    |  profile:    apps
fargate-ip-192-168-191-115.us-west-2.compute.internal  |  us-west-2b  |  FARGATE    |  profile:    apps
ip-192-168-100-194.us-west-2.compute.internal          |  us-west-2c  |  KARPENTER  |  nodepool:   apps
ip-192-168-155-246.us-west-2.compute.internal          |  us-west-2a  |  KARPENTER  |  nodepool:   apps
...
ip-192-168-173-151.us-west-2.compute.internal          |  us-west-2b  |  KARPENTER  |  nodepool:   apps
ip-192-168-28-67.us-west-2.compute.internal            |  us-west-2c  |  ON_DEMAND  |  apps-mng
ip-192-168-51-140.us-west-2.compute.internal           |  us-west-2a  |  ON_DEMAND  |  apps-mng
ip-192-168-83-58.us-west-2.compute.internal            |  us-west-2b  |  ON_DEMAND  |  apps-mng
ip-192-168-26-158.us-west-2.compute.internal           |  us-west-2c  |  ON_DEMAND  |  system-mng  
ip-192-168-33-46.us-west-2.compute.internal            |  us-west-2a  |  ON_DEMAND  |  system-mng  
ip-192-168-86-255.us-west-2.compute.internal           |  us-west-2b  |  ON_DEMAND  |  system-mng`

➤ Verify that all the components of the application are deployed as described in the table above:

`export DAEMONSETS_PODS=$(kubectl get ds -n kube-system -o json | jq -r '[.items[].metadata.name] | join ("\\|")')
kubectl get pods -n apps -o wide | grep -v "${DAEMONSETS_PODS}"`

Now that we have an overall view of the application, we can start the migration process by enabling the EKS Auto Mode for the cluster.

# Enabling EKS Auto Mode

[Configuring the Cluster](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/40-migrations/20-enabling-eks-auto-mode#configuring-cluster) | [Configuring EKS Auto Mode](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/40-migrations/20-enabling-eks-auto-mode#configuring-eks-auto-mode) | [Preparing the Application](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/40-migrations/20-enabling-eks-auto-mode#preparing-app)

---

## **Configuring the Cluster**

Before we enable EKS Auto Mode on our cluster we need to adjust certain IAM permissions to ensure its proper operation, which include:

1. Adjust the cluster's IAM role trust policy and permissions
2. Create an IAM role for the EKS Auto Mode worker nodes

We will explore these permissions in more detail in the following sections.

[**1. Update the Cluster IAM Role**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/40-migrations/20-enabling-eks-auto-mode#1.-update-the-cluster-iam-role)

EKS Auto Mode includes several Kubernetes capabilities as core components. These components, that would otherwise have to be managed as add-ons or self-managed controllers, include built-in support for Pod IP address assignments, Pod network policies, local DNS services, GPU plug-ins, health checkers, and EBS CSI storage.

To manage these components and ensure their function, EKS Auto Mode requires additional permissions, those that would, for non-EKS Auto Mode clusters, be provided directly to these add-ons and controllers and are now a part of the cluster IAM role.

As we've see in one of the previous sections, [EKS Auto Mode docs](https://docs.aws.amazon.com/eks/latest/userguide/auto-cluster-iam-role.html)  describe IAM policies to be added to the cluster role, in addition to the already existing `AmazonEKSClusterPolicy`:

- [AmazonEKSComputePolicy](https://docs.aws.amazon.com/aws-managed-policy/latest/reference/AmazonEKSComputePolicy.html)
- [AmazonEKSBlockStoragePolicy](https://docs.aws.amazon.com/aws-managed-policy/latest/reference/AmazonEKSBlockStoragePolicy.html)
- [AmazonEKSNetworkingPolicy](https://docs.aws.amazon.com/aws-managed-policy/latest/reference/AmazonEKSNetworkingPolicy.html)
- [AmazonEKSLoadBalancingPolicy](https://docs.aws.amazon.com/aws-managed-policy/latest/reference/AmazonEKSLoadBalancingPolicy.html)

In addition, EKS Auto Mode requires `sts:TagSession` action to be added to the cluster IAM role’s trust policy (you can view its current state in the IAM console).

➤ Create a trust policy JSON file:

`cat << EOF > trust-policy.json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Service": "eks.amazonaws.com"
            },
            "Action": [
                "sts:AssumeRole",
                "sts:TagSession"
            ]
        }
    ]
}
EOF`

➤ Update the cluster IAM role and remove the `trust-policy.json` file:

`aws iam update-assume-role-policy \
  --role-name ${MIGRATION_CLUSTER_ROLE_NAME} \
  --policy-document file://trust-policy.json

rm trust-policy.json`

➤ Add the required permissions to the cluster IAM role by executing:

`for POLICY_ARN in \
  "arn:aws:iam::aws:policy/AmazonEKSComputePolicy" \
  "arn:aws:iam::aws:policy/AmazonEKSBlockStoragePolicy" \
  "arn:aws:iam::aws:policy/AmazonEKSLoadBalancingPolicy" \
  "arn:aws:iam::aws:policy/AmazonEKSNetworkingPolicy"
do
  echo "Attaching policy ${POLICY_ARN} to IAM role ${MIGRATION_CLUSTER_ROLE_NAME}..."
  aws iam attach-role-policy --role-name ${MIGRATION_CLUSTER_ROLE_NAME} \
    --policy-arn ${POLICY_ARN}
done`

➤ Verify that the IAM role has been updated properly:

`aws iam get-role --role-name ${MIGRATION_CLUSTER_ROLE_NAME} | \
  jq -r '.Role.AssumeRolePolicyDocument.Statement[].Action[]'

aws iam list-attached-role-policies --role-name ${MIGRATION_CLUSTER_ROLE_NAME} | \
  jq -r '.AttachedPolicies[].PolicyName'`

The output should be (note the `AmazonEKSClusterPolicy` that the role already had attached before):

`sts:AssumeRole
sts:TagSession
AmazonEKSClusterPolicy
AmazonEKSNetworkingPolicy
AmazonEKSComputePolicy
AmazonEKSBlockStoragePolicy
AmazonEKSLoadBalancingPolicy`

[**2. Create the Node IAM Role**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/40-migrations/20-enabling-eks-auto-mode#2.-create-the-node-iam-role)

A Node IAM role contains the minimal permissions required for EKS components (kubelet and Pod Identity agent) to perform their function.

➤ Create a trust policy JSON file:

`cat << EOF > trust-policy.json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Service": "ec2.amazonaws.com"
            },
            "Action": [
                "sts:AssumeRole"
            ]
        }
    ]
}
EOF`

➤ Create the Node IAM role, store its ARN in an environment variable and remove the `trust-policy.json` file:

`aws iam create-role \
  --role-name ${MIGRATION_CLUSTER_NAME}-auto-mode-node-role \
  --assume-role-policy-document file://trust-policy.json

rm trust-policy.json`

➤ Attach the required policies:

`for POLICY_ARN in \
  "arn:aws:iam::aws:policy/AmazonEKSWorkerNodeMinimalPolicy" \
  "arn:aws:iam::aws:policy/AmazonEC2ContainerRegistryPullOnly"
do
  echo "Attaching policy ${POLICY_ARN} to IAM role ${MIGRATION_CLUSTER_NAME}-auto-mode-node-role..."
  aws iam attach-role-policy --role-name ${MIGRATION_CLUSTER_NAME}-auto-mode-node-role \
    --policy-arn ${POLICY_ARN}
done`

➤ Verify the created (or existing) role, its trust policy and attached managed policies:

`aws iam get-role \
  --role-name ${MIGRATION_CLUSTER_NAME}-auto-mode-node-role | \
  jq -r '.Role.AssumeRolePolicyDocument.Statement[].Action'

aws iam list-attached-role-policies \
  --role-name ${MIGRATION_CLUSTER_NAME}-auto-mode-node-role | \
  jq -r '.AttachedPolicies[].PolicyName'`

The command above should produce the following output:

`sts:AssumeRole
AmazonEKSWorkerNodeMinimalPolicy
AmazonEC2ContainerRegistryPullOnly`

We can now enable EKS Auto Mode.

[**3. Enable Amazon EKS Auto Mode**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/40-migrations/20-enabling-eks-auto-mode#3.-enable-amazon-eks-auto-mode)

➤ Define the node role ARN as an environment variable:

`export NODE_ROLE_ARN=$(aws iam get-role \
  --role-name ${MIGRATION_CLUSTER_NAME}-auto-mode-node-role \
  --query "Role.Arn" --output text)`

➤ Execute the following command to enable EKS Auto Mode (and verify that there are no errors in the output):

`aws eks update-cluster-config \
  --region ${AWS_REGION} \
  --name ${MIGRATION_CLUSTER_NAME} \
  --compute-config "{\"nodeRoleArn\": \"${NODE_ROLE_ARN}\", \"nodePools\": [\"system\"], \"enabled\": true}" \
  --kubernetes-network-config '{"elasticLoadBalancing":{"enabled": true}}' \
  --storage-config '{"blockStorage":{"enabled": true}}'`

➤ After 5 - 10 seconds, execute the following command to wait for the cluster EKS Auto Mode to become enabled:

`aws eks wait cluster-active --name ${MIGRATION_CLUSTER_NAME}`

You can also verify that the process of enabling EKS Auto Mode has started by navigating to the [AWS EKS console](https://console.aws.amazon.com/eks/home#/clusters) , navigating to the **migration** cluster and making sure that the corresponding panel looks like this (note the spinning icon on the Manage button):

![](https://static.us-east-1.prod.workshops.aws/7c3be994-d644-4401-a817-8cd56d557506/static/images/migration/eks-auto-mode-progress.png?Key-Pair-Id=K36Q2WVO3JP7QD&Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9zdGF0aWMudXMtZWFzdC0xLnByb2Qud29ya3Nob3BzLmF3cy83YzNiZTk5NC1kNjQ0LTQ0MDEtYTgxNy04Y2Q1NmQ1NTc1MDYvKiIsIkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTc0OTA3NDM0NH19fV19&Signature=W6WTuafMUQvUflH%7EEhZzuRyjNJftCEdrCF0ejl38MozYLykI2mAetYKbF86h0RLLnGofroTZPhK4yllzqxsaaDSSyRgze9Fvpjk0Ms1L8UBqAyv4jFwndJaf%7E4fBxBzS2cHu3Rk0lLG4Xo5Cb8A9PVDycYG8E%7Ez0HoIo2kyXPShI1JRocSpKKGDl50WVnd%7EQ8pQrxUD3L-ENWiyWP3JiuvViPXvc8mUUlCiCY0u9Jk%7E0LFiQm68sCn44JqL07uXLX3MpmBTchq-uqZdXWv1w5pouYAg-w9wgD5az4UBmySpxyRIPWFycxq4Gdy08r-AkurESWkXfjl3Bh%7EDkAPvLDg__)

After a couple of minutes the cluster should enable EKS Auto Mode:

![](https://static.us-east-1.prod.workshops.aws/7c3be994-d644-4401-a817-8cd56d557506/static/images/migration/eks-auto-mode-enabled.png?Key-Pair-Id=K36Q2WVO3JP7QD&Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9zdGF0aWMudXMtZWFzdC0xLnByb2Qud29ya3Nob3BzLmF3cy83YzNiZTk5NC1kNjQ0LTQ0MDEtYTgxNy04Y2Q1NmQ1NTc1MDYvKiIsIkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTc0OTA3NDM0NH19fV19&Signature=W6WTuafMUQvUflH%7EEhZzuRyjNJftCEdrCF0ejl38MozYLykI2mAetYKbF86h0RLLnGofroTZPhK4yllzqxsaaDSSyRgze9Fvpjk0Ms1L8UBqAyv4jFwndJaf%7E4fBxBzS2cHu3Rk0lLG4Xo5Cb8A9PVDycYG8E%7Ez0HoIo2kyXPShI1JRocSpKKGDl50WVnd%7EQ8pQrxUD3L-ENWiyWP3JiuvViPXvc8mUUlCiCY0u9Jk%7E0LFiQm68sCn44JqL07uXLX3MpmBTchq-uqZdXWv1w5pouYAg-w9wgD5az4UBmySpxyRIPWFycxq4Gdy08r-AkurESWkXfjl3Bh%7EDkAPvLDg__)

Before we proceed with migrations lets make sure the Auto Mode Karpenter configuration exist in the cluster.

➤ Verify that all node pools (including those managed by the self-managed Karpenter) and node classes are fully operational (READY=True):

`kubectl get nodepool,nodeclass,ec2nodeclass`

You should see an output, similar to the following, that shows the original self-managed Karpenter NodePool and EC2NodeClass, as well as the EKS Auto Mode NodePool and (a new CRD) NodeClass:

`NAME                           NODECLASS   NODES   READY   AGE
nodepool.karpenter.sh/apps     apps        8       True    89m
nodepool.karpenter.sh/system   default     0       True    8m47s

NAME                                  ROLE                                    READY   AGE
nodeclass.eks.amazonaws.com/default   migration-cluster-auto-mode-node-role   True    8m47s

NAME                                  READY   AGE
ec2nodeclass.karpenter.k8s.aws/apps   True    89m`

We are now ready to start the migration process of our applications to EKS Auto Mode-managed instances.

## **Configuring EKS Auto Mode**

EKS Auto Mode manages most infrastructure components automatically, while allowing customization to better fit the needs of the workloads.

EKS Auto Mode includes two built-in NodePools (and a NodeClass) that define how the cluster compute capacity is provisioned, out of the box:

- the `system` node pool, which is intended for cluster-critical applications, and
- the `general-purpose` node pool

While the `general-purpose` would work for most of the general applications' needs and help customers to get started (as you have seen in the [Getting Started](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/module-2-fundamentals/10-compute/10-getting-started) section of one of the previous modules), for the purposes of the migration we will use a different node pool.

Note that we opted out of creating the `general-purpose` node pool in the `update-cluster-config` command above.

We will use the configuration of the `apps` node pool we already have as a starting point, with some minor adjustments, to create a new custom node pool for EKS Auto Mode.

Note that EKS Auto Mode doesn’t allow changing the `general-purpose` node pool and the corresponding `default` node class. Hence, it is recommended to analyze the Kubernetes scheduling constraints that are in use such as labels, taints and tolerations, affinity and anti-affinity rules and create EKS Auto Mode node pools accordingly.

[**Create a Custom EKS Auto Mode Configuration (NodeClass and NodePool)**](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/40-migrations/20-enabling-eks-auto-mode#create-a-custom-eks-auto-mode-configuration-(nodeclass-and-nodepool))

➤ Create the `apps-auto-mode-np.yml` file:

`cat << EOF > apps-auto-mode-np.yml
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
  name: apps-auto-mode
spec:
  disruption:
    consolidationPolicy: WhenEmptyOrUnderutilized
    consolidateAfter: 30s
  template:
    metadata:
      labels:
        role: apps-auto-mode
    spec:
      nodeClassRef:
        group: eks.amazonaws.com
        kind: NodeClass
        name: default
      taints:
        - key: role
          value: apps-auto-mode
          effect: NoSchedule
      requirements:
        - key: kubernetes.io/arch
          operator: In
          values: [amd64, arm64]
        - key: kubernetes.io/os
          operator: In
          values: [linux]
        - key: karpenter.sh/capacity-type
          operator: In
          values: [on-demand]
        - key: eks.amazonaws.com/instance-category
          operator: In
          values: [c, m, r]
        - key: eks.amazonaws.com/instance-generation
          operator: Gt
          values: ["4"]
EOF`

To adjust the `apps` NodePool to EKS Auto Mode we’ve introduced the following changes:

1. renamed the node pool to `apps-auto-mode`
2. changed the node class reference to the EKS Auto Mode default NodeClass
3. renamed the label and the taint values to `apps-auto-mode`
4. removed the `karpenter.k8s.aws/instance-generation` as it is restricted by EKS Auto Mode

➤ Deploy the node pool:

`kubectl apply -f apps-auto-mode-np.yml`

➤ Verify that all node pools and node classes are fully operational (READY=True):

`kubectl get nodepool,nodeclass,ec2nodeclass`

Note that at that point no instances are registered with any of the node pools:

`NAME                                   NODECLASS   NODES   READY   AGE
nodepool.karpenter.sh/apps             apps        8       True    92m
nodepool.karpenter.sh/apps-auto-mode   default     0       True    56s
nodepool.karpenter.sh/system           default     0       True    12m

NAME                                  ROLE                                    READY   AGE
nodeclass.eks.amazonaws.com/default   migration-cluster-auto-mode-node-role   True    12m

NAME                                  READY   AGE
ec2nodeclass.karpenter.k8s.aws/apps   True    92m`

## **A Note on Preparing the Application**

Before applying any changes we need to ensure that the components in the cluster can withstand them with minimal impact. If we were to simply delete the nodes, all Pods associated with the nodes would be terminated and need to be re-scheduled at the same time, causing disruption to their services.

In Kubernetes, there are several ways of [controlling the disruptions](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/#dealing-with-disruptions)  and the decision which to apply depends on the [type of disruption](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/#voluntary-and-involuntary-disruptions)  we are about to introduce.

These ways are [PodDisruptionBudgets](https://kubernetes.io/docs/tasks/run-application/configure-pdb/)  and [Deployment strategy](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#strategy) .

Since our application components are deployed using Helm, which updates the Deployment resource, we will use a Deployment strategy, which is already included in our application components and looks like this:

`...
strategy:
  rollingUpdate:
    maxUnavailable: 1
  type: RollingUpdate...`

Note that while the above strategy suits our needs in context of the workshop, for your applications you should create strategies that matches your applications' requirements.

In addition to ensuring a controlled migration process above, we also need to migrate the network resources created by/for the application components.

Our retail store demo application defines an [Ingress](https://github.com/aws-containers/retail-store-sample-app/blob/main/deploy/kubernetes/charts/ui/templates/ingress.yaml)  resource to expose its components to external traffic.

This Ingress is then handled by the self-managed AWS Load Balancer Controller to provision the Application Load Balancer above and define rules according to the Ingress definitions.

We will discuss migrating the network components in greater details in a dedicated section further in the workshop, but the process will rely on DNS migration from a current setup to a network path we will create by leveraging the EKS Auto Mode load balancing capabilities.

With EKS Auto Mode enabled and the application prepared, we can move to migrating the application components, compute option by compute option.

# Migrating from AWS Fargate

[Migrate the Assets Component](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/40-migrations/30-migrating-from-fargate#migrate-assets-component)

---

In this section of the module we will demonstrate how to migrate applications deployed in Fargate to EKS Auto Mode using the `assets` component of our retail store application.

We will update the component to migrate to EKS Auto Mode by adding the relevant node selector and tolerations to align with the requirements defined in the `apps-auto-mode` EKS Auto Mode node pool.

Make sure you check the application health and availability by visiting the application load balancer URL from a browser and adding few items to the cart.

You can access the application UI by executing the following command to extract the Application Load Balancer DNS name and Ctrl/Cmd-clicking on the URL in the output:

`kubectl get ingress -n apps retail-store-app-ui-main \
  -o jsonpath="http://{.status.loadBalancer.ingress[*].hostname}{'\n'}"`

## **Migrate the `assets` Component**

➤ Observe the current state of the assets component:

`kubectl get pods -n apps -l app.kubernetes.io/instance=retail-store-app-assets -o wide`

The output should show, similar to the below, that the `assets` component is currently hosted exclusively on Fargate nodes.

`NAME                                       READY   STATUS    RESTARTS   AGE     IP            NODE                                                   NOMINATED NODE   READINESS GATES
retail-store-app-assets-5d5d9d9dfc-7wc6s   1/1     Running   0          3h29m   10.0.74.111   fargate-ip-10-0-74-111.eu-central-1.compute.internal   <none>           <none>
retail-store-app-assets-5d5d9d9dfc-fkks2   1/1     Running   0          3h24m   10.0.85.172   fargate-ip-10-0-85-172.eu-central-1.compute.internal   <none>           <none>
retail-store-app-assets-5d5d9d9dfc-mhw9h   1/1     Running   0          3h24m   10.0.49.132   fargate-ip-10-0-49-132.eu-central-1.compute.internal   <none>           <none>`

➤ You can review the distribution of instances across all capacity types by executing the following command:

`kubectl get nodes -o json | jq -r '.items[].metadata.labels | ."kubernetes.io/hostname" + " | " + ."topology.kubernetes.io/zone" + " | " + (."eks.amazonaws.com/capacityType" // if ."eks.amazonaws.com/compute-type" == "fargate" then "FARGATE" else "KARPENTER" end) + " | " + (."eks.amazonaws.com/nodegroup" // if ."karpenter.sh/nodepool" then "nodepool: " + ."karpenter.sh/nodepool" else "profile: apps" end)' | column -t | sort -k 5`

The command output should show the Fargate instances that host the `assets` component above:

`fargate-ip-192-168-116-56.us-west-2.compute.internal   |  us-west-2c  |  FARGATE    |  profile:    apps
fargate-ip-192-168-180-168.us-west-2.compute.internal  |  us-west-2b  |  FARGATE    |  profile:    apps
fargate-ip-192-168-191-115.us-west-2.compute.internal  |  us-west-2b  |  FARGATE    |  profile:    apps
ip-192-168-103-128.us-west-2.compute.internal          |  us-west-2c  |  KARPENTER  |  nodepool:   apps
ip-192-168-114-228.us-west-2.compute.internal          |  us-west-2c  |  KARPENTER  |  nodepool:   apps
ip-192-168-127-58.us-west-2.compute.internal           |  us-west-2c  |  KARPENTER  |  nodepool:   apps
ip-192-168-175-162.us-west-2.compute.internal          |  us-west-2b  |  KARPENTER  |  nodepool:   apps
ip-192-168-28-67.us-west-2.compute.internal            |  us-west-2c  |  ON_DEMAND  |  apps-mng
ip-192-168-51-140.us-west-2.compute.internal           |  us-west-2a  |  ON_DEMAND  |  apps-mng
ip-192-168-83-58.us-west-2.compute.internal            |  us-west-2b  |  ON_DEMAND  |  apps-mng
ip-192-168-26-158.us-west-2.compute.internal           |  us-west-2c  |  ON_DEMAND  |  system-mng  
ip-192-168-33-46.us-west-2.compute.internal            |  us-west-2a  |  ON_DEMAND  |  system-mng  
ip-192-168-86-255.us-west-2.compute.internal           |  us-west-2b  |  ON_DEMAND  |  system-mng`

➤ Create the `assets-values.yml` file for the `assets` component (see [here](https://github.com/aws-containers/retail-store-sample-app/blob/main/deploy/kubernetes/charts/assets/values.yaml)  for the whole `values.yml` file):

`cat << EOF > assets-values.yml
replicaCount: 3

podAnnotations:
  eks.amazonaws.com/compute-type: ec2

nodeSelector:
  role: apps-auto-mode

tolerations:
  - key: role
    value: apps-auto-mode
    operator: Equal
    effect: NoSchedule
EOF`

To ensure that the `assets` components are hosted on instances provisioned through the EKS Auto Mode node pool we defined in the previous section, we've added the corresponding node selector and tolerations.

Note that we added a Pod annotation: `eks.amazonaws.com/compute-type` above to ensure that Pods currently deployed on Fargate instances would gradually migrate to EKS Auto Mode.

Had we created the node selector only, without specifying the annotation, the Pods would be terminated and remained in the `Pending` state, since the `apps` Fargate profile instances do not have the corresponding label.

Alternatively, had we deleted the `apps` Fargate profile, that would cause all `assets` Pods to be terminated and scheduled at the same time, causing disruption to the application's services.

➤ In a separate VS Code terminal, execute the following command to observe the migration process:

`kubectl get pods -n apps -l app.kubernetes.io/name=assets -w`

➤ Update the `assets` component:

`1
2
3
4
5
helm upgrade retail-store-app-assets oci://public.ecr.aws/aws-containers/retail-store-sample-assets-chart \
  --version ${RETAIL_STORE_APP_HELM_CHART_VERSION} \
  --namespace apps \
  --values assets-values.yml \
  --wait`

➤ Observe that the application remains operational, while the component is being migrated, by navigating to the application UI, Ctrl/Cmd-click the URL in the output, and adding a couple of items to the cart:

`kubectl get ingress -n apps retail-store-app-ui-main \
  -o jsonpath="http://{.status.loadBalancer.ingress[*].hostname}{'\n'}"`

➤ After a couple of minutes, verify that all `assets` Pods are scheduled on the `apps-auto-mode` node pool by executing:

`export APPS_KARPENTER_AUTO_MODE_NODES=$(kubectl get nodes -o json | jq -r '[.items[].metadata.labels | select(."karpenter.sh/nodepool" == "apps-auto-mode") | ."kubernetes.io/hostname"] | join("\\|")')
kubectl get pods -n apps -l app.kubernetes.io/instance=retail-store-app-assets -o wide | grep "${APPS_KARPENTER_AUTO_MODE_NODES}"`

➤ You can, once more, review the distribution of instances across all capacity types by executing the following command and observing the change (removal of Fargate nodes and a new type of nodes provisioned via EKS Auto Mode `apps-auto-mode` node pool)

`kubectl get nodes -o json | jq -r '.items[].metadata.labels | ."kubernetes.io/hostname" + " | " + ."topology.kubernetes.io/zone" + " | " + (."eks.amazonaws.com/capacityType" // if ."eks.amazonaws.com/compute-type" == "fargate" then "FARGATE" else "KARPENTER" end) + " | " + (."eks.amazonaws.com/nodegroup" // if ."karpenter.sh/nodepool" then "nodepool: " + ."karpenter.sh/nodepool" else "profile: apps" end)' | column -t | sort -k 5`

# Migrating from EKS Managed Node Groups

[Migrate the Orders Component](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/40-migrations/40-migrating-from-mng#migrate-orders-component) | [Migrate the Catalog Component](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/40-migrations/40-migrating-from-mng#migrate-catalog-component)

---

In this section of the module we will migrate the `orders`, `catalog`, `orders` PostgreSQL database, `catalog`’s MySQL database and the RabbitMQ application components that are deployed onto apps-mng managed node group.

We will update these components to migrate to EKS Auto Mode by adding the relevant node selector and tolerations to align with the requirements defined in the `apps-auto-mode` EKS Auto Mode node pool.

## **Migrate the `orders` Component**

➤ Create the `orders-values.yml` file for the orders component (see [here](https://github.com/aws-containers/retail-store-sample-app/blob/main/deploy/kubernetes/charts/orders/values.yaml)  for the whole `values.yml` file):

`1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
cat << EOF > orders-values.yml
replicaCount: 3

nodeSelector:
  role: apps-auto-mode

tolerations:
  - key: role
    value: apps-auto-mode
    operator: Equal
    effect: NoSchedule

postgresql:
  nodeSelector:
    role: apps-auto-mode
  tolerations:
    - key: role
      value: apps-auto-mode
      operator: Equal
      effect: NoSchedule

rabbitmq:
  nodeSelector:
    role: apps-auto-mode
  tolerations:
    - key: role
      value: apps-auto-mode
      operator: Equal
      effect: NoSchedule
EOF`

➤ In a separate VS Code terminal, execute the following command to observe the migration process:

`kubectl get pods -n apps -l app.kubernetes.io/name=orders -w`

➤ Update the `orders` component:

`1
2
3
4
5
6
helm upgrade retail-store-app-orders oci://public.ecr.aws/aws-containers/retail-store-sample-orders-chart \
  --version ${RETAIL_STORE_APP_HELM_CHART_VERSION} \
  --namespace apps \
  --values orders-values.yml \
  --reuse-values \
  --wait`

➤ After a couple of minutes, verify that all `orders` Pods are scheduled on the `apps-auto-mode` nodes by executing:

`export APPS_KARPENTER_AUTO_MODE_NODES=$(kubectl get nodes -o json | jq -r '[.items[].metadata.labels | select(."karpenter.sh/nodepool" == "apps-auto-mode") | ."kubernetes.io/hostname"] | join("\\|")')
kubectl get pods -n apps -l app.kubernetes.io/instance=retail-store-app-orders -o wide | grep "${APPS_KARPENTER_AUTO_MODE_NODES}"`

## **Migrate the `catalog` Component**

➤ Create the `catalog-values.yml` file for the catalog component (see [here](https://github.com/aws-containers/retail-store-sample-app/blob/main/deploy/kubernetes/charts/catalog/values.yaml)  for the whole `values.yml` file):

`1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
cat << EOF > catalog-values.yml
replicaCount: 3

nodeSelector:
  role: apps-auto-mode

tolerations:
  - key: role
    value: apps-auto-mode
    operator: Equal
    effect: NoSchedule

mysql:
  nodeSelector:
    role: apps-auto-mode
  tolerations:
    - key: role
      value: apps-auto-mode
      operator: Equal
      effect: NoSchedule
EOF`

➤ In a separate VS Code terminal, execute the following command to observe the migration process:

`kubectl get pods -n apps -l app.kubernetes.io/name=catalog -w`

➤ Update the `catalog` component:

`1
2
3
4
5
6
helm upgrade retail-store-app-catalog oci://public.ecr.aws/aws-containers/retail-store-sample-catalog-chart \
  --version ${RETAIL_STORE_APP_HELM_CHART_VERSION} \
  --namespace apps \
  --values catalog-values.yml \
  --reuse-values \
  --wait`

➤ After a couple of minutes, verify that all `catalog` Pods are scheduled on the `apps-auto-mode` nodes by executing:

`export APPS_KARPENTER_AUTO_MODE_NODES=$(kubectl get nodes -o json | jq -r '[.items[].metadata.labels | select(."karpenter.sh/nodepool" == "apps-auto-mode") | ."kubernetes.io/hostname"] | join("\\|")')
kubectl get pods -n apps -l app.kubernetes.io/instance=retail-store-app-catalog -o wide | grep "${APPS_KARPENTER_AUTO_MODE_NODES}"`

➤ You can review the distribution of instances across all capacity types by executing the following command and observing the change (more instances provisioned via EKS Auto Mode `apps-auto-mode` node pool):

`kubectl get nodes -o json | jq -r '.items[].metadata.labels | ."kubernetes.io/hostname" + " | " + ."topology.kubernetes.io/zone" + " | " + (."eks.amazonaws.com/capacityType" // if ."eks.amazonaws.com/compute-type" == "fargate" then "FARGATE" else "KARPENTER" end) + " | " + (."eks.amazonaws.com/nodegroup" // if ."karpenter.sh/nodepool" then "nodepool: " + ."karpenter.sh/nodepool" else "profile: apps" end)' | column -t | sort -k 5`

# Migrating from a Self-Managed Karpenter

[Migrate the Checkout Component](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/40-migrations/50-migrating-from-karpenter#migrate-checkout-component) | [Migrate the Carts Component](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/40-migrations/50-migrating-from-karpenter#migrate-carts-component) | [Migrate the UI Component](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/40-migrations/50-migrating-from-karpenter#migrate-ui-component)

---

In this section of the module we will demonstrate how to migrate applications from a self-managed Karpenter to EKS Auto Mode.

In the current setup, the self-managed Karpenter controller handles the compute requirements for the `checkout`, `carts`, and UI components of the retail store application.

We will update these components to migrate to EKS Auto Mode by adding the relevant node selector and tolerations to align with the requirements defined in the `apps-auto-mode` EKS Auto Mode node pool.

## **Migrate the `checkout` Component**

➤ Create the `checkout-values.yml` file for the `checkout` component (see [here](https://github.com/aws-containers/retail-store-sample-app/blob/main/deploy/kubernetes/charts/checkout/values.yaml)  for the whole `values.yml` file):

`1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
cat << EOF > checkout-values.yml
replicaCount: 3

nodeSelector:
  role: apps-auto-mode

tolerations:
  - key: role
    value: apps-auto-mode
    operator: Equal
    effect: NoSchedule

redis:
  nodeSelector:
    role: apps-auto-mode
  tolerations:
    - key: role
      value: apps-auto-mode
      operator: Equal
      effect: NoSchedule
EOF`

➤ In a separate VS Code terminal, execute the following command to observe the migration process:

`kubectl get pods -n apps -l app.kubernetes.io/name=checkout -w`

➤ Update the `checkout` component:

`1
2
3
4
5
helm upgrade retail-store-app-checkout oci://public.ecr.aws/aws-containers/retail-store-sample-checkout-chart \
  --version ${RETAIL_STORE_APP_HELM_CHART_VERSION} \
  --namespace apps \
  --values checkout-values.yml \
  --wait`

➤ After a couple of minutes, verify that all `checkout` Pods are scheduled on the `apps-auto-mode` nodes by executing:

`export APPS_KARPENTER_AUTO_MODE_NODES=$(kubectl get nodes -o json | jq -r '[.items[].metadata.labels | select(."karpenter.sh/nodepool" == "apps-auto-mode") | ."kubernetes.io/hostname"] | join("\\|")')
kubectl get pods -n apps -l app.kubernetes.io/instance=retail-store-app-checkout -o wide | grep "${APPS_KARPENTER_AUTO_MODE_NODES}"`

## **Migrate the `carts` Component**

➤ Create the `carts-values.yml` file for the `carts` component (see [here](https://github.com/aws-containers/retail-store-sample-app/blob/main/deploy/kubernetes/charts/carts/values.yaml)  for the whole `values.yml` file):

`1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
cat << EOF > carts-values.yml
replicaCount: 3

nodeSelector:
  role: apps-auto-mode

tolerations:
  - key: role
    value: apps-auto-mode
    operator: Equal
    effect: NoSchedule

dynamodb:
  nodeSelector:
    role: apps-auto-mode
  tolerations:
    - key: role
      value: apps-auto-mode
      operator: Equal
      effect: NoSchedule
EOF`

➤ In a separate VS Code terminal, execute the following command to observe the migration process:

`kubectl get pods -n apps -l app.kubernetes.io/name=carts -w`

➤ Update the `carts` component:

`1
2
3
4
5
helm upgrade retail-store-app-carts oci://public.ecr.aws/aws-containers/retail-store-sample-cart-chart \
  --version ${RETAIL_STORE_APP_HELM_CHART_VERSION} \
  --namespace apps \
  --values carts-values.yml \
  --wait`

➤ After a couple of minutes, verify that all `carts` Pods are scheduled on the `apps-auto-mode` nodes by executing:

`export APPS_KARPENTER_AUTO_MODE_NODES=$(kubectl get nodes -o json | jq -r '[.items[].metadata.labels | select(."karpenter.sh/nodepool" == "apps-auto-mode") | ."kubernetes.io/hostname"] | join("\\|")')
kubectl get pods -n apps -l app.kubernetes.io/instance=retail-store-app-carts -o wide | grep "${APPS_KARPENTER_AUTO_MODE_NODES}"`

## **Migrate the UI Component**

➤ Create the `ui-values.yml` file for the UI component (see [here](https://github.com/aws-containers/retail-store-sample-app/blob/main/deploy/kubernetes/charts/ui/values.yaml)  for the whole `values.yml` file):

`1
2
3
4
5
6
7
8
9
10
11
12
cat << EOF > ui-values.yml
replicaCount: 3

nodeSelector:
  role: apps-auto-mode

tolerations:
  - key: role
    value: apps-auto-mode
    operator: Equal
    effect: NoSchedule
EOF`

➤ In a separate VS Code terminal, execute the following command to observe the migration process:

`kubectl get pods -n apps -l app.kubernetes.io/name=ui -w`

➤ Update the UI component:

`1
2
3
4
5
6
helm upgrade retail-store-app-ui oci://public.ecr.aws/aws-containers/retail-store-sample-ui-chart \
  --version ${RETAIL_STORE_APP_HELM_CHART_VERSION} \
  --namespace apps \
  --values ui-values.yml \
  --reuse-values \
  --wait`

➤ After a couple of minutes, verify that all `ui` Pods are scheduled on the `apps-auto-mode` nodes by executing:

`export APPS_KARPENTER_AUTO_MODE_NODES=$(kubectl get nodes -o json | jq -r '[.items[].metadata.labels | select(."karpenter.sh/nodepool" == "apps-auto-mode") | ."kubernetes.io/hostname"] | join("\\|")')
kubectl get pods -n apps -l app.kubernetes.io/instance=retail-store-app-ui -o wide | grep "${APPS_KARPENTER_AUTO_MODE_NODES}"`

At this point all application Pods should run on EKS Auto Mode managed instances. Let's verify that.

➤ View the all the Pods (excluding DaemonSets) and their nodes by executing the following command:

`export DAEMONSETS_PODS=$(kubectl get ds -n kube-system -o json | jq -r '[.items[].metadata.name] | join ("\\|")')
kubectl get pods -A -o wide | grep -v "${DAEMONSETS_PODS}"`

We can omit DaemonSets to reduce the visual clutter, since they, by themselves, do not impact the compute distribution.

This should provide an output similar to the following (omitting the EKS Auto Mode instances for brevity):

`NAMESPACE     NAME                                               READY   STATUS    RESTARTS        AGE     IP                NODE                                           NOMINATED NODE   READINESS GATES
apps          retail-store-app-assets-66ddb94d9d-82rwz           1/1     Running   0               68s     192.168.178.193   i-08144b8a087c03470                            <none>           <none>
apps          retail-store-app-assets-66ddb94d9d-qj8vs           1/1     Running   0               2m55s   192.168.11.129    i-0744bcd2550cdfe3c                            <none>           <none>
apps          retail-store-app-assets-66ddb94d9d-r65h6           1/1     Running   0               2m54s   192.168.43.197    i-0aa138324ce6086d2                            <none>           <none>
...
kube-system   aws-load-balancer-controller-8c9657c99-c4hw4       1/1     Running   0               121m    192.168.41.16     ip-192-168-33-46.us-west-2.compute.internal    <none>           <none>
kube-system   aws-load-balancer-controller-8c9657c99-hhwdv       1/1     Running   0               121m    192.168.69.64     ip-192-168-86-255.us-west-2.compute.internal   <none>           <none>
kube-system   coredns-6d5c5bdb9f-2t2pw                           1/1     Running   0               130m    192.168.90.238    ip-192-168-86-255.us-west-2.compute.internal   <none>           <none>
kube-system   coredns-6d5c5bdb9f-7jswn                           1/1     Running   0               130m    192.168.94.40     ip-192-168-86-255.us-west-2.compute.internal   <none>           <none>
kube-system   karpenter-b677796f8-2n998                          1/1     Running   0               121m    192.168.31.184    ip-192-168-26-158.us-west-2.compute.internal   <none>           <none>
kube-system   karpenter-b677796f8-x5clj                          1/1     Running   0               121m    192.168.53.232    ip-192-168-33-46.us-west-2.compute.internal    <none>           <none>
kube-system   metrics-server-7d99f5f76c-6xz9f                    1/1     Running   0               130m    192.168.72.50     ip-192-168-86-255.us-west-2.compute.internal   <none>           <none>
kube-system   metrics-server-7d99f5f76c-zkpxg                    1/1     Running   0               130m    192.168.70.163    ip-192-168-86-255.us-west-2.compute.internal   <none>           <none>`

You can see that all application components' Pods in the `apps` namespace are running on EKS Auto Mode instances (identified by their `i-xxxxxxxxxxxxxxxxx` name) and the cluster operation software, controllers and add-ons, are not.

➤ View the distribution of instances across capacity types:

`kubectl get nodes -o json | jq -r '.items[].metadata.labels | ."kubernetes.io/hostname" + " | " + ."topology.kubernetes.io/zone" + " | " + (."eks.amazonaws.com/capacityType" // if ."eks.amazonaws.com/compute-type" == "fargate" then "FARGATE" else "KARPENTER" end) + " | " + (."eks.amazonaws.com/nodegroup" // if ."karpenter.sh/nodepool" then "nodepool: " + ."karpenter.sh/nodepool" else "profile: apps" end)' | column -t | sort -k 5`

The result should be similar to the following:

`i-00e094708c70292a0                           |  us-west-2b  |  KARPENTER  |  nodepool:   apps-auto-mode
i-03abf23d3f63c45dc                           |  us-west-2b  |  KARPENTER  |  nodepool:   apps-auto-mode
i-0744bcd2550cdfe3c                           |  us-west-2c  |  KARPENTER  |  nodepool:   apps-auto-mode
i-08144b8a087c03470                           |  us-west-2b  |  KARPENTER  |  nodepool:   apps-auto-mode
i-0aa138324ce6086d2                           |  us-west-2a  |  KARPENTER  |  nodepool:   apps-auto-mode
...
ip-192-168-28-67.us-west-2.compute.internal   |  us-west-2c  |  ON_DEMAND  |  apps-mng
ip-192-168-51-140.us-west-2.compute.internal  |  us-west-2a  |  ON_DEMAND  |  apps-mng
ip-192-168-83-58.us-west-2.compute.internal   |  us-west-2b  |  ON_DEMAND  |  apps-mng
ip-192-168-26-158.us-west-2.compute.internal  |  us-west-2c  |  ON_DEMAND  |  system-mng  
ip-192-168-33-46.us-west-2.compute.internal   |  us-west-2a  |  ON_DEMAND  |  system-mng  
ip-192-168-86-255.us-west-2.compute.internal  |  us-west-2b  |  ON_DEMAND  |  system-mng`

Note that you may continue to see the `apps` node pool with its now empty nodes, while Karpenter terminates them.

You can, from the Pods output and from that distribution of instances across compute options, verify that only `system-mng` nodes (`ip-192-168-26-158...`, `ip-192-168-33-46...`, `ip-192-168-86-255...`) actually host any non-DaemonSet Pods, as we successfully migrated all the application components Pods to EKS Auto Mode.

# Migrating Networking Resources

[Create New Load Balancers](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/40-migrations/60-migrating-networking-resources#create-elb) | [Migrate to the New Load Balancers](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/40-migrations/60-migrating-networking-resources#migrate-to-elb)

---

In this section, we will demonstrate how to migrate networking resources, specifically AWS Application Load Balancer (ALB) and Network Load Balancer (NLB).

When using the AWS Load Balancer Controller, as we did in our [setup](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/module-9-migration/10-cluster-configuration#overview), creating a Kubernetes Ingress resource automatically provisions an AWS Application Load Balancer (ALB), while creating a Kubernetes Service resource of type `LoadBalancer` provisions an AWS Network Load Balancer (NLB) for application traffic distribution.

## **Create New Load Balancers**

In our workshop setup, the UI application is configured with a Kubernetes Ingress resource and is accessible through an AWS Application Load Balancer (ALB).

You can access the application UI by executing the following command to extract the Application Load Balancer DNS name and Ctrl/Cmd-clicking on the URL in the output:

`kubectl get ingress -n apps retail-store-app-ui-main \
  -o jsonpath="http://{.status.loadBalancer.ingress[*].hostname}{'\n'}"`

When migrating applications that use LoadBalancers to EKS Auto Mode, you must create new load balancers, as existing ones, managed by the self-managed AWS Load Balancer controller, cannot be migrated to EKS Auto Mode.

See [here](https://docs.aws.amazon.com/eks/latest/userguide/migrate-auto.html)  for additional information on migrating resources on in existing Amazon EKS clusters.

In the UI component Helm implementation, we have defined Ingress resources as [an array](https://github.com/aws-containers/retail-store-sample-app/blob/main/deploy/kubernetes/charts/ui/values.yaml#L98-L103) , enabling us to create a new Ingress resource, while maintaining the existing Ingress-created ALB during migration.

➤ View the application's Ingress resources:

`kubectl get ingress -n apps`

If you're not using Helm, we recommend creating a new Ingress resource with a different name that uses the Ingress className created specifically for EKS Auto Mode.

So, before proceeding with the migration, we will create a new IngressClass.

This set up makes sure that the necessary infrastructure configurations are in place to support ingress requirements for applications that are deployed later. Typically, this is a step performed by the platform team once after the cluster is created.

➤ Define the new IngressClass:

`cat << EOF > ingress-class.yml
apiVersion: eks.amazonaws.com/v1
kind: IngressClassParams
metadata:
  name: eks-auto-mode-alb
spec:
  scheme: internet-facing
---
apiVersion: networking.k8s.io/v1
kind: IngressClass
metadata:
  name: eks-auto-mode-alb
spec:
  controller: eks.amazonaws.com/alb
  parameters:
    apiGroup: eks.amazonaws.com
    kind: IngressClassParams
    name: eks-auto-mode-alb
EOF`

➤ Deploy the IngressClass:

`kubectl apply -f ingress-class.yml`

With EKS Auto Mode enabled and the application prepared, we can move to migrating the application components, compute option by compute option.

In the following Helm configuration we are doing exactly that, by using a new IngressClass with the `className: eks-auto-alb` for the second Ingress resource definition.

➤ Create the `ui-ingress-values.yml` file for the UI component (see [here](https://github.com/aws-containers/retail-store-sample-app/blob/main/deploy/kubernetes/charts/ui/values.yaml)  for the whole `values.yml` file):

`1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
cat << EOF > ui-ingress-values.yml
ingresses:
  - enabled: **true**
    className: alb
    name: main
    annotations:
      alb.ingress.kubernetes.io/scheme: internet-facing
      alb.ingress.kubernetes.io/target-type: ip
  - enabled: **true**
    className: eks-auto-mode-alb
    name: main-auto-mode
    annotations:
      alb.ingress.kubernetes.io/scheme: internet-facing
      alb.ingress.kubernetes.io/target-type: ip
EOF`

Note that we need to define both the old and the new Ingress resources, in our case, to avoid overriding the original configuration.

➤ Update the UI component:

`1
2
3
4
5
6
helm upgrade retail-store-app-ui oci://public.ecr.aws/aws-containers/retail-store-sample-ui-chart \
  --version ${RETAIL_STORE_APP_HELM_CHART_VERSION} \
  --namespace apps \
  --values ui-ingress-values.yml \
  --reuse-values \
  --wait`

➤ Verify that there are now two Ingress resource:

`kubectl get ingress -n apps`

➤ After a couple of minutes, verify that you can access the application UI, via the **new** ALB by executing the following command to extract the DNS name and Ctrl/Cmd-clicking on the URL in the output:

`kubectl get ingress -n apps retail-store-app-ui-main-auto-mode \
  -o jsonpath="http://{.status.loadBalancer.ingress[*].hostname}{'\n'}"`

➤ Also verify that you can access the application UI, via the **old** ALB by executing the following command to extract the DNS name and Ctrl/Cmd-clicking on the URL in the output:

`kubectl get ingress -n apps retail-store-app-ui-main \
  -o jsonpath="http://{.status.loadBalancer.ingress[*].hostname}{'\n'}"`

## **Migrate to the New Load Balancers**

To ensure a successful migration, several best practices must be followed.

Schedule migrations during low-traffic periods and implement a DNS-based migration strategy for zero downtime.

EKS Auto Mode maintains compatibility with [external-dns](https://github.com/kubernetes-sigs/external-dns) , which automatically registers new load balancers with Route 53. If you're not using `external-dns`, you'll need to update DNS entries either manually or through automation.

During the migration period, it is essential to maintain both the old and the new load balancers while continuously monitoring performance metrics.

Have a comprehensive rollback plan ready for any unexpected issues.

Once testing confirms a successful migration, you can remove the old load balancer by deleting its Ingress resource. In this example, we'll execute a helm upgrade to update the ingress array, removing the old ingress entry.

➤ Create the `ui-single-ingress-values.yml` file:

`1
2
3
4
5
6
7
8
9
cat << EOF > ui-single-ingress-values.yml
ingresses:
  - enabled: **true**
    className: eks-auto-mode-alb
    name: main-auto-mode
    annotations:
      alb.ingress.kubernetes.io/scheme: internet-facing
      alb.ingress.kubernetes.io/target-type: ip
EOF`

Note that array above removes the second Ingress resource by overriding the entire `ingresses` array.

➤ Update the UI component:

`1
2
3
4
5
6
helm upgrade retail-store-app-ui oci://public.ecr.aws/aws-containers/retail-store-sample-ui-chart \
  --version ${RETAIL_STORE_APP_HELM_CHART_VERSION} \
  --namespace apps \
  --values ui-single-ingress-values.yml \
  --reuse-values \
  --wait`

➤ After a couple of minutes, verify that only one Ingress resource remains:

`kubectl get ingress -n apps`

➤ Verify that you can access the application UI, via the **new** ALB by executing the following command to extract the DNS name and Ctrl/Cmd-clicking on the URL in the output:

`kubectl get ingress -n apps retail-store-app-ui-main-auto-mode \
  -o jsonpath="http://{.status.loadBalancer.ingress[*].hostname}{'\n'}"`

➤ Verify that you no longer can retrieve the **old** ALB (expected to receive error):

`kubectl get ingress -n apps retail-store-app-ui-main \
  -o jsonpath="http://{.status.loadBalancer.ingress[*].hostname}{'\n'}"`

Note that SSL certificates can be shared between your old and new load balancers. However, ensure that your certificate is configured with an appropriate Subject Alternative Names (SANs) that match all domains served by both ALBs, particularly if you're changing domain names during migration.

Server Name Indication (SNI) enables this functionality, allowing the ALB to select the correct certificate based on the client's requested hostname.

We have now migrated our retail store application to EKS Auto Mode and all that remains is to remove the no-longer-required add-ons and compute resources.

# Removing non-EKS Auto Mode Add-ons and Compute

[Uninstall Karpenter](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/40-migrations/80-handling-cluster-addons#uninstall-karpenter) | [Uninstall the AWS Load Balancer Controller](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/40-migrations/80-handling-cluster-addons#uninstall-lbc) | [Remove the Amazon EKS Add-ons](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/40-migrations/80-handling-cluster-addons#remove-addons) | [Delete the Managed Node Groups](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/40-migrations/80-handling-cluster-addons#delete-mng)

---

After migrating to EKS Auto Mode, which includes several Kubernetes capabilities as core components we no longer require the following components and compute options:

- The AWS Fargate `apps` profile
- The `apps-mng` managed node group
- The `system-mng` managed node group
- The CoreDNS add-on
- The Amazon VPC CNI add-on
- The kube-proxy add-on
- The EBS CSI Driver add-on
- The EKS Pod Identity Agent add-on
- The self-managed AWS Load Balancer Controller
- The self-managed Karpenter

We will now remove these components from the **migration** cluster.

## **Uninstall the Self-Managed AWS Load Balancer Controller**

➤ Uninstall AWS Load Balancer Controller Helm chart and delete its CRDs:

`helm uninstall --namespace kube-system aws-load-balancer-controller
kubectl delete -k "github.com/aws/eks-charts/stable/aws-load-balancer-controller/crds?ref=master"`

➤ Extract AWS Load Balancer controller role Pod identity association:

`export LBC_POD_IDENTITY_ASSOCIATION_ID=$(aws eks list-pod-identity-associations \
  --cluster-name ${MIGRATION_CLUSTER_NAME} \
  --namespace kube-system \
  --service-account aws-load-balancer-controller \
  --query 'associations[*].associationId' \
  --output text)`

➤ Detach and delete AWS Load Balancer Controller policy:

`export LBC_ROLE_NAME=$(aws eks describe-pod-identity-association \
  --cluster-name ${MIGRATION_CLUSTER_NAME} \
  --association-id ${LBC_POD_IDENTITY_ASSOCIATION_ID} | jq -r '.association.roleArn | split("/") | .[1]')

export LBC_POLICY_ARN=$(aws iam list-attached-role-policies \
  --role-name ${LBC_ROLE_NAME} | \
  jq -r '.AttachedPolicies[].PolicyArn')

aws iam detach-role-policy \
    --role-name ${LBC_ROLE_NAME} \
    --policy-arn ${LBC_POLICY_ARN}

aws iam delete-policy \
    --policy-arn ${LBC_POLICY_ARN}`

➤ Delete the Pod identity association:

`aws eks delete-pod-identity-association \
  --cluster-name ${MIGRATION_CLUSTER_NAME} \
  --association-id ${LBC_POD_IDENTITY_ASSOCIATION_ID}`

## **Uninstall the Self-Managed Karpenter**

➤ Verify that there are no self-managed Karpenter-created nodes:

`kubectl get nodes -o json | jq -r '.items[].metadata.labels | ."kubernetes.io/hostname" + " | " + ."topology.kubernetes.io/zone" + " | " + (."eks.amazonaws.com/capacityType" // if ."eks.amazonaws.com/compute-type" == "fargate" then "FARGATE" else "KARPENTER" end) + " | " + (."eks.amazonaws.com/nodegroup" // if ."karpenter.sh/nodepool" then "nodepool: " + ."karpenter.sh/nodepool" else "profile: apps" end)' | column -t | sort -k 5`

➤ Delete the NodePool and NodeClass:

`kubectl delete nodepool apps
kubectl delete ec2nodeclass apps`

➤ Uninstall Karpenter:

`helm uninstall --namespace kube-system karpenter`

➤ Delete self-managed Karpenter nodes access entry:

`aws eks delete-access-entry \
  --cluster-name ${MIGRATION_CLUSTER_NAME} \
  --principal-arn arn:aws:iam::${AWS_ACCOUNT_ID}:role/KarpenterNodeRole-${MIGRATION_CLUSTER_NAME}`

➤ Extract Karpenter role Pod identity association:

`export KARPENTER_POD_IDENTITY_ASSOCIATION_ID=$(aws eks list-pod-identity-associations \
  --cluster-name ${MIGRATION_CLUSTER_NAME} \
  --namespace kube-system \
  --service-account karpenter \
  --query 'associations[*].associationId' \
  --output text)`

➤ Extract Karpenter controller role name:

`export KARPENTER_ROLE_NAME=$(aws eks describe-pod-identity-association \
  --cluster-name ${MIGRATION_CLUSTER_NAME} \
  --association-id ${KARPENTER_POD_IDENTITY_ASSOCIATION_ID} | jq -r '.association.roleArn | split("/") | .[1]')`

➤ Detach Karpenter policy:

`aws iam detach-role-policy \
  --role-name ${KARPENTER_ROLE_NAME} \
  --policy-arn arn:aws:iam::${AWS_ACCOUNT_ID}:policy/KarpenterControllerPolicy-${MIGRATION_CLUSTER_NAME}`

➤ Delete the Pod identity association:

`aws eks delete-pod-identity-association \
  --cluster-name ${MIGRATION_CLUSTER_NAME} \
  --association-id ${KARPENTER_POD_IDENTITY_ASSOCIATION_ID}`

➤ Remove Karpenter-related instance profiles:

`KARPENTER_NODE_ROLE=KarpenterNodeRole-${MIGRATION_CLUSTER_NAME}
KARPENTER_INSTANCE_PROFILES=$(aws iam list-instance-profiles-for-role \
  --role-name ${KARPENTER_NODE_ROLE} \
  --query 'InstanceProfiles[*].InstanceProfileName' \
  --output text)

for profile in ${KARPENTER_INSTANCE_PROFILES}; do
  echo "Removing role from instance profile ${profile}"
  aws iam remove-role-from-instance-profile --instance-profile-name "${profile}" --role-name ${KARPENTER_NODE_ROLE}
  echo "Deleting instance profile ${profile}"
  aws iam delete-instance-profile --instance-profile-name "${profile}"
done`

➤ Delete Karpenter role:

`aws iam delete-role --role-name ${KARPENTER_ROLE_NAME}`

➤ Remove Karpenter-related resources:

`aws cloudformation delete-stack --stack-name Karpenter-${MIGRATION_CLUSTER_NAME}
aws cloudformation wait stack-delete-complete --stack-name Karpenter-${MIGRATION_CLUSTER_NAME}

aws ec2 describe-launch-templates --filters "Name=tag:karpenter.k8s.aws/cluster,Values=${MIGRATION_CLUSTER_NAME}" |
    jq -r ".LaunchTemplates[].LaunchTemplateName" |
    xargs -I{} aws ec2 delete-launch-template --launch-template-name {}`

## **Remove the Unnecessary Amazon EKS Add-ons**

➤ Remove the no-longer-required Amazon EKS Add-ons:

`aws eks delete-addon --cluster-name ${MIGRATION_CLUSTER_NAME} --addon-name coredns
aws eks delete-addon --cluster-name ${MIGRATION_CLUSTER_NAME} --addon-name vpc-cni
aws eks delete-addon --cluster-name ${MIGRATION_CLUSTER_NAME} --addon-name kube-proxy
aws eks delete-addon --cluster-name ${MIGRATION_CLUSTER_NAME} --addon-name aws-ebs-csi-driver
aws eks delete-addon --cluster-name ${MIGRATION_CLUSTER_NAME} --addon-name eks-pod-identity-agent`

## **Delete the Managed Node Groups**

We have now successfully migrated the application and removed all the unnecessary controllers and add-ons and thus we no longer require either of the managed node groups.

➤ Delete the node groups:

`eksctl delete nodegroup \
  --region ${AWS_REGION} \
  --cluster ${MIGRATION_CLUSTER_NAME} \
  --name=apps-mng

eksctl delete nodegroup \
  --region ${AWS_REGION} \
  --cluster ${MIGRATION_CLUSTER_NAME} \
  --name=system-mng`

Removal of the node groups and termination of their instances may take a couple of minutes.

➤ Verify that all non-EKS Auto Mode compute options were removed:

`kubectl get nodes -o json | jq -r '.items[].metadata.labels | ."kubernetes.io/hostname" + " | " + ."topology.kubernetes.io/zone" + " | " + (."eks.amazonaws.com/capacityType" // if ."eks.amazonaws.com/compute-type" == "fargate" then "FARGATE" else "KARPENTER" end) + " | " + (."eks.amazonaws.com/nodegroup" // if ."karpenter.sh/nodepool" then "nodepool: " + ."karpenter.sh/nodepool" else "profile: apps" end)' | column -t | sort -k 5`

Note that we've created the node groups using eksctl, so your process may slightly differ.

# Cleanup Environment

If you have run the workshop **In your own AWS Account** it is recommended to clean up resources so no extra costs will occur.

Sign-in in to the AWS Management Console, make sure to change to the AWS Region you deployed the workshop in, use the Region selector in the upper-right corner of the page.

## **1. Delete the `eks-automode-workshop` CloudFormation Stack**

1. Navigate to the [AWS CloudFormation console](https://console.aws.amazon.com/cloudformation)
2. In the Navigation pane, choose **Stacks**.
3. Search for the `eks-automode-workshop` Stack.
4. Choose the `eks-automode-workshop` Stack and Click **Delete**, a popup will open, click **Delete**.Deleting the `eks-automode-workshop` stack will automatically delete all the additional stacks created as part of it.
5. Deletion is completed when you are no longer able to see the `eks-automode-workshop` stack and all its related stacks.

**Note**

This process might take a while (approximately 30 minutes).

**Delete the CloudFormation Stack**

## **2. Module 2: EBS Storage - Delete EBS volumes used by the demo cluster.**

1. Navigate to the [Amazon Elastic Compute Cloud (EC2) console](https://console.aws.amazon.com/ec2)
2. In the Navigation pane, choose **Volumes**.
3. **Search** and **Select** the EBS volumes provisioned by the EBS CSI driver, you can use the search filter `KubernetesCluster = demo-cluster`
4. Choose **Actions**, and choose **Delete Volume**.
5. To confirm deletion, type `delete` in the field, and then click **Delete**.

**Delete the EBS volumes**

## **3. Module 2: EBS Storage - Delete the AWS Key Management Service (KMS) key**

1. Navigate to the [AWS Key Management Service console](https://console.aws.amazon.com/kms)
2. In the Navigation pane, choose **Customer managed keys**.
3. Search and Select the KMS key created for the [default StorageClass encryption](https://catalog.us-east-1.prod.workshops.aws/event/dashboard/en-US/workshop/20-fundamentals/30-storage/20-storage-class##create-a-default-storageclass-with-kms-encryption), you can use the search filter `Name = eks-automode-workshop`
4. Choose **Key actions**, and choose **Schedule key deletion**.
5. (Optional) Reduce the waiting period to a minimum of 7 days.
6. Ensure that the Keys to delete table only includes the keys from the workshop.
7. Select Confirm that you want to schedule these keys for deletion after a X day waiting period.
8. Click **Schedule deletion**.

**Delete the EBS KMS Key**

## **4. Module 4: Migration - Delete the migration cluster Node IAM Role**

1. Navigate to the [Amazon IAM Identity and Access Management (IAM) console](https://console.aws.amazon.com/iam)
2. In the Navigation pane, choose **Roles**
3. In the Search bar, Search for `migration-cluster-auto-mode-node-role`
4. Select the Node IAM Role and Choose **Delete**.
5. Confirm deletion by entering the role name in the text input field and click **Delete**.

**Delete the Node IAM Role**

