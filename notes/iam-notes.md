EEOrganizations role is mapped to policy AdministratorAccess
which is 

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "*",
            "Resource": "*"
        }
    ]
}
```
with following trust relation

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::328397449223:root"
            },
            "Action": "sts:AssumeRole"
        },
        {
            "Sid": "EEControlPlaneAccountTrust",
            "Effect": "Allow",
            "Principal": {
                "AWS": [
                    "arn:aws:iam::122334600246:root",
                    "arn:aws:iam::572239370997:root"
                ]
            },
            "Action": "sts:AssumeRole",
            "Condition": {
                "StringEquals": {
                    "sts:ExternalId": "31e56e4cdf4d47a1a36c3542f8b3e5f7"
                }
            }
        }
    ]
}
```

WSOpsRole has following policy, WSOpsRolePermissionsPolicy

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```
with following trust relation
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "WSOpsRoleTrust",
            "Effect": "Allow",
            "Principal": {
                "AWS": [
                    "arn:aws:iam::484654583263:root",
                    "arn:aws:iam::338779401994:user/WSControlPlaneUser"
                ]
            },
            "Action": "sts:AssumeRole"
        }
    ]
}
```

Role WSParticipantRole is mapped to AdministratorAccess policy and ws-default-policy
ws-default-policy is as follows 
``` 
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowIamReadOnly",
            "Effect": "Allow",
            "Action": [
                "iam:List*",
                "iam:Get*",
                "iam:Generate*",
                "sts:GetCallerIdentity"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Sid": "AllowCreateSLR",
            "Effect": "Allow",
            "Action": [
                "iam:CreateServiceLinkedRole"
            ],
            "Resource": [
                "arn:aws:iam::*:role/aws-service-role/*"
            ]
        },
        {
            "Sid": "AllowIamPassRole",
            "Effect": "Allow",
            "Action": [
                "iam:PassRole"
            ],
            "Resource": [
                "arn:aws:iam::338779401994:role/WSParticipantRole"
            ]
        },
        {
            "Sid": "DenyAllOutsideAllowedRegions",
            "Effect": "Deny",
            "NotAction": [
                "iam:*",
                "sts:*",
                "s3:*",
                "ds:*",
                "artifact:Get",
                "artifact:DownloadAgreement",
                "lightsail:*",
                "networkmanager:*",
                "braket:*",
                "quicksight:*",
                "cloudfront:*",
                "route53:*",
                "route53-recovery-cluster:*",
                "route53-recovery-control-config:*",
                "route53-recovery-readiness:*",
                "servicediscovery:*",
                "waf:*",
                "waf-regional:*",
                "wafv2:*",
                "cloudwatch:DescribeAlarms",
                "cloudwatch:PutMetricAlarm",
                "cloudwatch:DeleteAlarms",
                "cloudwatch:GetMetricStatistics",
                "elasticloadbalancing:DescribeLoadBalancers",
                "ec2:Describe*",
                "ecr:GetDownloadUrlForLayer",
                "ecr:BatchGetImage",
                "ecr:BatchCheckLayerAvailability",
                "ecr:GetAuthorizationToken",
                "globalaccelerator:*",
                "acm:List*",
                "acm:Describe*",
                "cloudformation:List*",
                "cloudformation:Describe*",
                "kms:Describe*",
                "kms:ReEncrypt*",
                "kms:GenerateDataKey*",
                "kms:Get*",
                "kms:List*",
                "kms:CreateGrant",
                "kms:RevokeGrant",
                "ssm:List*",
                "directconnect:*",
                "sso:List*",
                "sso:Describe*",
                "sso:Get*"
            ],
            "Resource": [
                "*"
            ],
            "Condition": {
                "StringNotEquals": {
                    "aws:RequestedRegion": [
                        "us-east-1"
                    ]
                }
            }
        }
    ]
}
```
with following trust policy
``` 
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "WSParticipantRoleTrust",
            "Effect": "Allow",
            "Principal": {
                "AWS": [
                    "arn:aws:iam::484654583263:root",
                    "arn:aws:iam::338779401994:user/WSControlPlaneUser"
                ]
            },
            "Action": "sts:AssumeRole"
        }
    ]
}
```

Role WSReaperRole is mapped to WSReaperRolePermissionsPolicy as below
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```

Role WSSystemRole with policy WSSystemRolePermissionsPolicy as below 
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "*"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


