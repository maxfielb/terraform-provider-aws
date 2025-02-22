---
subcategory: "Transfer Family"
layout: "aws"
page_title: "AWS: aws_transfer_server"
description: |-
  Provides a AWS Transfer Server resource.
---


<!-- Please do not edit this file, it is generated. -->
# Resource: aws_transfer_server

Provides a AWS Transfer Server resource.

~> **NOTE on AWS IAM permissions:** If the `endpointType` is set to `VPC`, the `ec2:DescribeVpcEndpoints` and `ec2:ModifyVpcEndpoint` [actions](https://docs.aws.amazon.com/service-authorization/latest/reference/list_amazonec2.html#amazonec2-actions-as-permissions) are used.

~> **NOTE:** Use the [`aws_transfer_tag`](transfer_tag.html) resource to manage the system tags used for [custom hostnames](https://docs.aws.amazon.com/transfer/latest/userguide/requirements-dns.html#tag-custom-hostname-cdk).

## Example Usage

### Basic

```typescript
// DO NOT EDIT. Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
import { Construct } from "constructs";
import { TerraformStack } from "cdktf";
/*
 * Provider bindings are generated by running `cdktf get`.
 * See https://cdk.tf/provider-generation for more details.
 */
import { TransferServer } from "./.gen/providers/aws/transfer-server";
class MyConvertedCode extends TerraformStack {
  constructor(scope: Construct, name: string) {
    super(scope, name);
    new TransferServer(this, "example", {
      tags: {
        Name: "Example",
      },
    });
  }
}

```

### Security Policy Name

```typescript
// DO NOT EDIT. Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
import { Construct } from "constructs";
import { TerraformStack } from "cdktf";
/*
 * Provider bindings are generated by running `cdktf get`.
 * See https://cdk.tf/provider-generation for more details.
 */
import { TransferServer } from "./.gen/providers/aws/transfer-server";
class MyConvertedCode extends TerraformStack {
  constructor(scope: Construct, name: string) {
    super(scope, name);
    new TransferServer(this, "example", {
      securityPolicyName: "TransferSecurityPolicy-2020-06",
    });
  }
}

```

### VPC Endpoint

```typescript
// DO NOT EDIT. Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
import { Construct } from "constructs";
import { Token, TerraformStack } from "cdktf";
/*
 * Provider bindings are generated by running `cdktf get`.
 * See https://cdk.tf/provider-generation for more details.
 */
import { TransferServer } from "./.gen/providers/aws/transfer-server";
class MyConvertedCode extends TerraformStack {
  constructor(scope: Construct, name: string) {
    super(scope, name);
    new TransferServer(this, "example", {
      endpointDetails: {
        addressAllocationIds: [Token.asString(awsEipExample.id)],
        subnetIds: [Token.asString(awsSubnetExample.id)],
        vpcId: Token.asString(awsVpcExample.id),
      },
      endpointType: "VPC",
    });
  }
}

```

### AWS Directory authentication

```typescript
// DO NOT EDIT. Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
import { Construct } from "constructs";
import { Token, TerraformStack } from "cdktf";
/*
 * Provider bindings are generated by running `cdktf get`.
 * See https://cdk.tf/provider-generation for more details.
 */
import { TransferServer } from "./.gen/providers/aws/transfer-server";
class MyConvertedCode extends TerraformStack {
  constructor(scope: Construct, name: string) {
    super(scope, name);
    new TransferServer(this, "example", {
      directoryId: Token.asString(awsDirectoryServiceDirectoryExample.id),
      identityProviderType: "AWS_DIRECTORY_SERVICE",
    });
  }
}

```

### AWS Lambda authentication

```typescript
// DO NOT EDIT. Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
import { Construct } from "constructs";
import { Token, TerraformStack } from "cdktf";
/*
 * Provider bindings are generated by running `cdktf get`.
 * See https://cdk.tf/provider-generation for more details.
 */
import { TransferServer } from "./.gen/providers/aws/transfer-server";
class MyConvertedCode extends TerraformStack {
  constructor(scope: Construct, name: string) {
    super(scope, name);
    new TransferServer(this, "example", {
      function: Token.asString(awsLambdaIdentityProviderExample.arn),
      identityProviderType: "AWS_LAMBDA",
    });
  }
}

```

### Protocols

```typescript
// DO NOT EDIT. Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
import { Construct } from "constructs";
import { Token, TerraformStack } from "cdktf";
/*
 * Provider bindings are generated by running `cdktf get`.
 * See https://cdk.tf/provider-generation for more details.
 */
import { TransferServer } from "./.gen/providers/aws/transfer-server";
class MyConvertedCode extends TerraformStack {
  constructor(scope: Construct, name: string) {
    super(scope, name);
    new TransferServer(this, "example", {
      certificate: Token.asString(awsAcmCertificateExample.arn),
      endpointDetails: {
        subnetIds: [Token.asString(awsSubnetExample.id)],
        vpcId: Token.asString(awsVpcExample.id),
      },
      endpointType: "VPC",
      identityProviderType: "API_GATEWAY",
      protocols: ["FTP", "FTPS"],
      url:
        "${" +
        awsApiGatewayDeploymentExample.invokeUrl +
        "${" +
        awsApiGatewayResourceExample.path +
        "}",
    });
  }
}

```

### Using Structured Logging Destinations

```typescript
// DO NOT EDIT. Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
import { Construct } from "constructs";
import { Token, TerraformStack } from "cdktf";
/*
 * Provider bindings are generated by running `cdktf get`.
 * See https://cdk.tf/provider-generation for more details.
 */
import { CloudwatchLogGroup } from "./.gen/providers/aws/cloudwatch-log-group";
import { DataAwsIamPolicyDocument } from "./.gen/providers/aws/data-aws-iam-policy-document";
import { IamRole } from "./.gen/providers/aws/iam-role";
import { TransferServer } from "./.gen/providers/aws/transfer-server";
class MyConvertedCode extends TerraformStack {
  constructor(scope: Construct, name: string) {
    super(scope, name);
    const transfer = new CloudwatchLogGroup(this, "transfer", {
      namePrefix: "transfer_test_",
    });
    const transferAssumeRole = new DataAwsIamPolicyDocument(
      this,
      "transfer_assume_role",
      {
        statement: [
          {
            actions: ["sts:AssumeRole"],
            effect: "Allow",
            principals: [
              {
                identifiers: ["transfer.amazonaws.com"],
                type: "Service",
              },
            ],
          },
        ],
      }
    );
    const iamForTransfer = new IamRole(this, "iam_for_transfer", {
      assumeRolePolicy: Token.asString(transferAssumeRole.json),
      managedPolicyArns: [
        "arn:aws:iam::aws:policy/service-role/AWSTransferLoggingAccess",
      ],
      namePrefix: "iam_for_transfer_",
    });
    const awsTransferServerTransfer = new TransferServer(this, "transfer_3", {
      endpointType: "PUBLIC",
      loggingRole: iamForTransfer.arn,
      protocols: ["SFTP"],
      structuredLogDestinations: ["${" + transfer.arn + "}:*"],
    });
    /*This allows the Terraform resource name to match the original name. You can remove the call if you don't need them to match.*/
    awsTransferServerTransfer.overrideLogicalId("transfer");
  }
}

```

## Argument Reference

This resource supports the following arguments:

* `certificate` - (Optional) The Amazon Resource Name (ARN) of the AWS Certificate Manager (ACM) certificate. This is required when `protocols` is set to `FTPS`
* `domain` - (Optional) The domain of the storage system that is used for file transfers. Valid values are: `S3` and `EFS`. The default value is `S3`.
* `protocols` - (Optional) Specifies the file transfer protocol or protocols over which your file transfer protocol client can connect to your server's endpoint. This defaults to `SFTP` . The available protocols are:
    * `AS2`: File transfer over Applicability Statement 2
    * `SFTP`: File transfer over SSH
    * `FTPS`: File transfer with TLS encryption
    * `FTP`: Unencrypted file transfer
* `endpointDetails` - (Optional) The virtual private cloud (VPC) endpoint settings that you want to configure for your SFTP server. Fields documented below.
* `endpointType` - (Optional) The type of endpoint that you want your SFTP server connect to. If you connect to a `VPC` (or `VPC_ENDPOINT`), your SFTP server isn't accessible over the public internet. If you want to connect your SFTP server via public internet, set `PUBLIC`.  Defaults to `PUBLIC`.
* `invocationRole` - (Optional) Amazon Resource Name (ARN) of the IAM role used to authenticate the user account with an `identityProviderType` of `API_GATEWAY`.
* `hostKey` - (Optional) RSA, ECDSA, or ED25519 private key (e.g., as generated by the `ssh-keygen -t rsa -b 2048 -N "" -m PEM -f my-new-server-key`, `ssh-keygen -t ecdsa -b 256 -N "" -m PEM -f my-new-server-key` or `ssh-keygen -t ed25519 -N "" -f my-new-server-key` commands).
* `url` - (Optional) - URL of the service endpoint used to authenticate users with an `identityProviderType` of `API_GATEWAY`.
* `identityProviderType` - (Optional) The mode of authentication enabled for this service. The default value is `SERVICE_MANAGED`, which allows you to store and access SFTP user credentials within the service. `API_GATEWAY` indicates that user authentication requires a call to an API Gateway endpoint URL provided by you to integrate an identity provider of your choice. Using `AWS_DIRECTORY_SERVICE` will allow for authentication against AWS Managed Active Directory or Microsoft Active Directory in your on-premises environment, or in AWS using AD Connectors. Use the `AWS_LAMBDA` value to directly use a Lambda function as your identity provider. If you choose this value, you must specify the ARN for the lambda function in the `function` argument.
* `directoryId` - (Optional) The directory service ID of the directory service you want to connect to with an `identityProviderType` of `AWS_DIRECTORY_SERVICE`.
* `function` - (Optional) The ARN for a lambda function to use for the Identity provider.
* `loggingRole` - (Optional) Amazon Resource Name (ARN) of an IAM role that allows the service to write your SFTP users’ activity to your Amazon CloudWatch logs for monitoring and auditing purposes.
* `forceDestroy` - (Optional) A boolean that indicates all users associated with the server should be deleted so that the Server can be destroyed without error. The default value is `false`. This option only applies to servers configured with a `SERVICE_MANAGED` `identityProviderType`.
* `postAuthenticationLoginBanner`- (Optional) Specify a string to display when users connect to a server. This string is displayed after the user authenticates. The SFTP protocol does not support post-authentication display banners.
* `preAuthenticationLoginBanner`- (Optional) Specify a string to display when users connect to a server. This string is displayed before the user authenticates.
* `protocolDetails`- (Optional) The protocol settings that are configured for your server.
* `securityPolicyName` - (Optional) Specifies the name of the security policy that is attached to the server. Possible values are `TransferSecurityPolicy-2018-11`, `TransferSecurityPolicy-2020-06`, `TransferSecurityPolicy-FIPS-2020-06`, `TransferSecurityPolicy-FIPS-2023-05`, `TransferSecurityPolicy-2022-03`, `TransferSecurityPolicy-2023-05`, `TransferSecurityPolicy-PQ-SSH-Experimental-2023-04` and `TransferSecurityPolicy-PQ-SSH-FIPS-Experimental-2023-04`. Default value is: `TransferSecurityPolicy-2018-11`.
* `structuredLogDestinations` - (Optional) A set of ARNs of destinations that will receive structured logs from the transfer server such as CloudWatch Log Group ARNs. If provided this enables the transfer server to emit structured logs to the specified locations.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider [`defaultTags` configuration block](https://registry.terraform.io/providers/hashicorp/aws/latest/docs#default_tags-configuration-block) present, tags with matching keys will overwrite those defined at the provider-level.
* `workflowDetails` - (Optional) Specifies the workflow details. See Workflow Details below.

### Endpoint Details

* `addressAllocationIds` - (Optional) A list of address allocation IDs that are required to attach an Elastic IP address to your SFTP server's endpoint. This property can only be used when `endpointType` is set to `VPC`.
* `securityGroupIds` - (Optional) A list of security groups IDs that are available to attach to your server's endpoint. If no security groups are specified, the VPC's default security groups are automatically assigned to your endpoint. This property can only be used when `endpointType` is set to `VPC`.
* `subnetIds` - (Optional) A list of subnet IDs that are required to host your SFTP server endpoint in your VPC. This property can only be used when `endpointType` is set to `VPC`.
* `vpcEndpointId` - (Optional) The ID of the VPC endpoint. This property can only be used when `endpointType` is set to `VPC_ENDPOINT`
* `vpcId` - (Optional) The VPC ID of the virtual private cloud in which the SFTP server's endpoint will be hosted. This property can only be used when `endpointType` is set to `VPC`.

### Protocol Details

* `as2Transports` - (Optional) Indicates the transport method for the AS2 messages. Currently, only `HTTP` is supported.
* `passiveIp` - (Optional) Indicates passive mode, for FTP and FTPS protocols. Enter a single IPv4 address, such as the public IP address of a firewall, router, or load balancer.
* `setStatOption` - (Optional) Use to ignore the error that is generated when the client attempts to use `SETSTAT` on a file you are uploading to an S3 bucket. Valid values: `DEFAULT`, `ENABLE_NO_OP`.
* `tlsSessionResumptionMode` - (Optional) A property used with Transfer Family servers that use the FTPS protocol. Provides a mechanism to resume or share a negotiated secret key between the control and data connection for an FTPS session. Valid values: `DISABLED`, `ENABLED`, `ENFORCED`.
  
### Workflow Details

* `onUpload` - (Optional) A trigger that starts a workflow: the workflow begins to execute after a file is uploaded. See Workflow Detail below.
* `onPartialUpload` - (Optional) A trigger that starts a workflow if a file is only partially uploaded. See Workflow Detail below.

#### Workflow Detail

* `executionRole` - (Required) Includes the necessary permissions for S3, EFS, and Lambda operations that Transfer can assume, so that all workflow steps can operate on the required resources.
* `workflowId` - (Required)  A unique identifier for the workflow.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - Amazon Resource Name (ARN) of Transfer Server
* `id`  - The Server ID of the Transfer Server (e.g., `s-12345678`)
* `endpoint` - The endpoint of the Transfer Server (e.g., `s-12345678.server.transfer.REGION.amazonaws.com`)
* `hostKeyFingerprint` - This value contains the message-digest algorithm (MD5) hash of the server's host key. This value is equivalent to the output of the `ssh-keygen -l -E md5 -f my-new-server-key` command.
* `tagsAll` - A map of tags assigned to the resource, including those inherited from the provider [`defaultTags` configuration block](https://registry.terraform.io/providers/hashicorp/aws/latest/docs#default_tags-configuration-block).

## Import

In Terraform v1.5.0 and later, use an [`import` block](https://developer.hashicorp.com/terraform/language/import) to import Transfer Servers using the server `id`. For example:

```typescript
// DO NOT EDIT. Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
import { Construct } from "constructs";
import { TerraformStack } from "cdktf";
/*
 * Provider bindings are generated by running `cdktf get`.
 * See https://cdk.tf/provider-generation for more details.
 */
import { TransferServer } from "./.gen/providers/aws/transfer-server";
class MyConvertedCode extends TerraformStack {
  constructor(scope: Construct, name: string) {
    super(scope, name);
    TransferServer.generateConfigForImport(this, "example", "s-12345678");
  }
}

```

Using `terraform import`, import Transfer Servers using the server `id`. For example:

```console
% terraform import aws_transfer_server.example s-12345678
```

Certain resource arguments, such as `hostKey`, cannot be read via the API and imported into Terraform. Terraform will display a difference for these arguments the first run after import if declared in the Terraform configuration for an imported resource.

<!-- cache-key: cdktf-0.20.1 input-b8182f2a6ac884ea727497d533e9abe149fd46cabc5bd2ce49bd5bd67a96760c -->