# rancher-k8s

## IAM permissions
Following IAM permissions are the minimum permissions needed for your IAM user or IAM role to create platform and cluster.
For jenkins deployment, create user with following policies and create jenkins secret `aws-credentials-devops` with aws_access_key_id and aws_secret_access_key.
  
1. Access to terraform state bucket

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "arn:aws:s3:::tdock-tfstate"
    },
    {
      "Effect": "Allow",
      "Action": ["s3:GetObject", "s3:PutObject"],
      "Resource": "arn:aws:s3:::tdock-tfstate/*"
    }
  ]
}
```

2. Create/update cloudformation stacks

```json
{
    "Version": "2012-10-17",
    "Statement": [
        { 
            "Sid": "cloudformation",
            "Effect": "Allow", 
            "Action": "cloudformation:*", 
            "Resource": "*",
            "Condition": { 
                "ForAllValues:StringEqualsIgnoreCase": {
                    "cloudformation:ImportResourceTypes": [ 
                        "AWS::EC2::SecurityGroup*" 
                    ] 
                } 
            } 
        } 
    ]
}
```

3. Get/Create/Update SSM parameters

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "SSM",
            "Effect": "Allow",
            "Action": [
                "ssm:DescribeParameters",
                "ssm:GetParameter",
                "ssm:GetParameterHistory",
                "ssm:GetParameters",
                "ssm:GetParametersByPath",
                "ssm:AddTagsToResource",
                "ssm:RemoveTagsFromResource",
                "ssm:DeleteParameter",
                "ssm:DeleteParameters",
                "ssm:LabelParameterVersion",
                "ssm:PutParameter",
                "ssm:ListTagsForResource"
            ],
            "Resource": "*"
        }
    ]
}
```
  
4. Create/Update an Certificate manager sertificate.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "ACM",
            "Effect": "Allow",
            "Action": [
                "acm:AddTagsToCertificate",
                "acm:DeleteCertificate",
                "acm:DescribeCertificate",
                "acm:GetCertificate",
                "acm:ListCertificates",
                "acm:ListTagsForCertificate",
                "acm:RemoveTagsFromCertificate",
                "acm:RequestCertificate",
                "route53:GetHostedZone",
                "route53:ListHostedZones",
                "route53:ListHostedZonesByName",
                "route53:ChangeResourceRecordSets",
                "route53:GetChange",
                "route53:ListResourceRecordSets"
            ],
            "Resource": "*"
        }
    ]
}
```

5. Create/Update security groups

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "SG",
            "Effect": "Allow",
            "Action": [
                "ec2:*SecurityGroup*"
            ],
            "Resource": "*"
        }
    ]
}
```

6. Create/update an EKS cluster.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "autoscaling:AttachInstances",
                "autoscaling:CreateAutoScalingGroup",
                "autoscaling:CreateLaunchConfiguration",
                "autoscaling:CreateOrUpdateTags",
                "autoscaling:DeleteAutoScalingGroup",
                "autoscaling:DeleteLaunchConfiguration",
                "autoscaling:DeleteTags",
                "autoscaling:Describe*",
                "autoscaling:DetachInstances",
                "autoscaling:SetDesiredCapacity",
                "autoscaling:UpdateAutoScalingGroup",
                "autoscaling:SuspendProcesses",
                "autoscaling:EnableMetricsCollection",
                "autoscaling:PutLifecycleHook",
                "ec2:AllocateAddress",
                "ec2:AssignPrivateIpAddresses",
                "ec2:Associate*",
                "ec2:AttachInternetGateway",
                "ec2:AttachNetworkInterface",
                "ec2:AuthorizeSecurityGroupEgress",
                "ec2:AuthorizeSecurityGroupIngress",
                "ec2:CreateDefaultSubnet",
                "ec2:CreateDhcpOptions",
                "ec2:CreateEgressOnlyInternetGateway",
                "ec2:CreateInternetGateway",
                "ec2:CreateNatGateway",
                "ec2:CreateNetworkInterface",
                "ec2:CreateRoute",
                "ec2:CreateRouteTable",
                "ec2:CreateSecurityGroup",
                "ec2:CreateSubnet",
                "ec2:CreateTags",
                "ec2:CreateVolume",
                "ec2:DeleteDhcpOptions",
                "ec2:DeleteEgressOnlyInternetGateway",
                "ec2:DeleteInternetGateway",
                "ec2:DeleteNatGateway",
                "ec2:DeleteNetworkInterface",
                "ec2:DeleteRoute",
                "ec2:DeleteRouteTable",
                "ec2:DeleteSecurityGroup",
                "ec2:DeleteSubnet",
                "ec2:DeleteTags",
                "ec2:DeleteVolume",
                "ec2:DeleteVpc",
                "ec2:DeleteVpnGateway",
                "ec2:Describe*",
                "ec2:DetachInternetGateway",
                "ec2:DetachNetworkInterface",
                "ec2:DetachVolume",
                "ec2:Disassociate*",
                "ec2:ModifySubnetAttribute",
                "ec2:ModifyVpcAttribute",
                "ec2:ModifyVpcEndpoint",
                "ec2:ReleaseAddress",
                "ec2:RevokeSecurityGroupEgress",
                "ec2:RevokeSecurityGroupIngress",
                "ec2:UpdateSecurityGroupRuleDescriptionsEgress",
                "ec2:UpdateSecurityGroupRuleDescriptionsIngress",
                "ec2:CreateLaunchTemplate",
                "ec2:CreateLaunchTemplateVersion",
                "ec2:DeleteLaunchTemplate",
                "ec2:DeleteLaunchTemplateVersions",
                "ec2:DescribeLaunchTemplates",
                "ec2:DescribeLaunchTemplateVersions",
                "ec2:GetLaunchTemplateData",
                "ec2:ModifyLaunchTemplate",
                "ec2:RunInstances",
                "eks:CreateCluster",
                "eks:DeleteCluster",
                "eks:DescribeCluster",
                "eks:ListClusters",
                "eks:UpdateClusterConfig",
                "eks:UpdateClusterVersion",
                "eks:DescribeUpdate",
                "eks:TagResource",
                "eks:UntagResource",
                "eks:ListTagsForResource",
                "eks:CreateFargateProfile",
                "eks:DeleteFargateProfile",
                "eks:DescribeFargateProfile",
                "eks:ListFargateProfiles",
                "eks:CreateNodegroup",
                "eks:DeleteNodegroup",
                "eks:DescribeNodegroup",
                "eks:ListNodegroups",
                "eks:UpdateNodegroupConfig",
                "eks:UpdateNodegroupVersion",
                "iam:AddRoleToInstanceProfile",
                "iam:AttachRolePolicy",
                "iam:CreateInstanceProfile",
                "iam:CreateOpenIDConnectProvider",
                "iam:CreateServiceLinkedRole",
                "iam:CreatePolicy",
                "iam:CreatePolicyVersion",
                "iam:CreateRole",
                "iam:DeleteInstanceProfile",
                "iam:DeleteOpenIDConnectProvider",
                "iam:DeletePolicy",
                "iam:DeleteRole",
                "iam:DeleteRolePolicy",
                "iam:DeleteServiceLinkedRole",
                "iam:DetachRolePolicy",
                "iam:GetInstanceProfile",
                "iam:GetOpenIDConnectProvider",
                "iam:GetPolicy",
                "iam:GetPolicyVersion",
                "iam:GetRole",
                "iam:GetRolePolicy",
                "iam:List*",
                "iam:PassRole",
                "iam:PutRolePolicy",
                "iam:RemoveRoleFromInstanceProfile",
                "iam:TagRole",
                "iam:UntagRole",
                "iam:UpdateAssumeRolePolicy",
                "elasticfilesystem:*",
                "logs:CreateLogGroup",
                "logs:DescribeLogGroups",
                "logs:DeleteLogGroup",
                "logs:ListTagsLogGroup",
                "logs:PutRetentionPolicy",
                "kms:CreateGrant",
                "kms:CreateKey",
                "kms:DescribeKey",
                "kms:GetKeyPolicy",
                "kms:GetKeyRotationStatus",
                "kms:ListResourceTags",
                "kms:ScheduleKeyDeletion",
                "kms:ListAliases",
                "kms:EnableKeyRotation",
                "kms:UpdateKeyDescription",
                "kms:CreateAlias",
                "route53:ListTagsForResource",
                "s3:Get*",
                "s3:List*",
                "s3:PutBucketTagging",
                "s3:CreateBucket",
                "s3:PutBucketAcl",
                "s3:PutBucketPolicy",
                "lambda:*",
                "events:*",
                "route53:TestDNSAnswer"
            ],
            "Resource": "*"
        }
    ]
}
```

## Using the workspace bucket to transfer files to and from the cluster

There is a bucket for each cluster and named `tdock-{CLUSTERNAME}-cluster-workspace` where `{CLUSTERNAME}` is the name of the cluster in Rancher.

It can be used to move files to and from Pods in the cluster.

You can use aws cli to interact with the S3 bucket either from the internet or from inside pods.

### Set up awscli inside Pods

Use the package manager appropriate for the container image to install `awscli` packege.
Cluster is configured to have access to S3 so you can use awscli without setting up any credentials.

### Set up awscli on your machine

Follow the instructions for your OS [here](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html).

You need to provide AWS credentials with permissions to access the cluster workspace bucket before using awscli.

### Commands for pushing and pulling

* Pushing files to bucket
`aws s3 cp path/to/local/file s3://tdock-{CLUSTERNAME}-cluster-workspace/path/in/bucket`

* Pulling files from bucket
`aws s3 cp s3://tdock-{CLUSTERNAME}-cluster-workspace/path/in/bucket path/to/local/file`

