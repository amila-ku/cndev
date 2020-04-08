---
title: Infrastructure as Real Code
date: 2019-04-30
hero: "/images/hero-6.jpg"
excerpt: Infrastructure as Real Code
timeToRead: 3
authors: []

---
Infrastructure as Code (IaC) is being widely accepted as the way forward to implement infrastructure. It gives the ability to reuse, version and test infrastructure as with any regular code. This approach made a huge difference in how infrastructure is managed, the ability to troubleshoot and recover/recreate infrastructure, enable better quality testing, improved efficiency, and predictable deployment, lovers the cost for experimentation, more predictable infrastructure deployments and decreases the meantime for resolution. There are a plethora of tools available to properly implement infrastructure as code and most of them are now grown to be well-oiled frameworks for defining infrastructure. These tools can be categorized into two, procedural and declarative. _Terraform, CloudFormation, Saltstack,_ and _Puppet_ being declarative and _Ansible_ and _Chef_ having a procedural approach. Deciding on which one is best for the job is more based on personal preference but Terraform has been very prominent due to its support for multiple clouds, reusability.

But when thinking about all this points to the question ‘Why do we have to learn yaml based syntax only for implementing Infrastructure as Code?’. And if you started with Cloudformation on AWS and you have to automate your infrastructure in Google Cloud or Azure you would have to learn YAML or JSON based new approach, Terraform would be a good alternative but hcl also has it’s limitations. What if we could define IaC in a regular programming language?.

Luckily there are several options

* [Pulumi](https://pulumi.io/quickstart/)
* [Metaparticle](https://github.com/metaparticle-io?language=go)
* [Ballerina](https://ballerina.io/)

In this article, we will go through how to set up an AWS Lambda function using Pulumi.

Installing

```js live
curl -fsSL https://get.pulumi.com | sh
```

verify installation

```js live
pulumi version
```

create new project using template

```js live
pulumi new hello-aws-javascript — dir lambda-pulumi
```

pulumi also provides a similar feature to ‘terraform plan’ with ‘pulumi preview’ command, let's create a project using the existing template

```js live
$ pulumi upwarning: A new version of Pulumi is available. To upgrade from version ‘0.16.14’ to ‘0.16.16’, run  $ curl -sSL https://get.pulumi.com | shor visit https://pulumi.io/install for manual instructions and release notes.Previewing update (dev):Type Name Plan  + pulumi:pulumi:Stack lambda-pulumi-dev create  + └─ aws:apigateway:x:API hello create  + ├─ aws:iam:Role hello4c238266 create  + ├─ aws:s3:Bucket hello create  + ├─ aws:iam:Role hello66382ec5 create  + ├─ aws:iam:RolePolicyAttachment hello4c238266 create  + ├─ aws:s3:BucketObject hello4c238266/index.html create  + ├─ aws:s3:BucketObject hello4c238266/favicon.png create  + ├─ aws:iam:RolePolicyAttachment hello66382ec5–32be53a2 create  + ├─ aws:lambda:Function hello66382ec5 create  + ├─ aws:apigateway:RestApi hello create  + ├─ aws:apigateway:Deployment hello create  + ├─ aws:lambda:Permission hello-f61e7551 create  + └─ aws:apigateway:Stage hello create  Resources: + 14 to createDo you want to perform this update? yesUpdating (dev):Type Name Status  + pulumi:pulumi:Stack lambda-pulumi-dev created  + └─ aws:apigateway:x:API hello created  + ├─ aws:iam:Role hello66382ec5 created  + ├─ aws:iam:Role hello4c238266 created  + ├─ aws:s3:Bucket hello created  + ├─ aws:iam:RolePolicyAttachment hello66382ec5–32be53a2 created  + ├─ aws:lambda:Function hello66382ec5 created  + ├─ aws:iam:RolePolicyAttachment hello4c238266 created  + ├─ aws:s3:BucketObject hello4c238266/index.html created  + ├─ aws:s3:BucketObject hello4c238266/favicon.png created  + ├─ aws:apigateway:RestApi hello created  + ├─ aws:apigateway:Deployment hello created  + ├─ aws:lambda:Permission hello-f61e7551 created  + └─ aws:apigateway:Stage hello created  Outputs: url: “https://t3tfwiiw1d.execute-api.us-east-1.amazonaws.com/stage/”Resources: + 14 createdDuration: 28sPermalink: https://app.pulumi.com/amila-ku/lambda-pulumi/dev/updates/3
```

pulumi has a similar feel to how terraform is used to define and create infrastructure. Also it stores project configuration and outputs centrally in Pulumi Dashboard, this information can be shared among friedns easily with this approach.

![](https://miro.medium.com/max/30/1*g5QH3tccjizT13eOV32yug.png?q=20 =1600x814)

![](https://miro.medium.com/max/1600/1*g5QH3tccjizT13eOV32yug.png =1600x814)

destroying the resources is also the same as with terraform and it will ask for confirmation before destroying the resources.

```js live
pulumi destroywarning: A new version of Pulumi is available. To upgrade from version ‘0.16.14’ to ‘0.16.16’, run  $ curl -sSL https://get.pulumi.com | shor visit https://pulumi.io/install for manual instructions and release notes.Previewing destroy (dev):Type Name Plan  — pulumi:pulumi:Stack lambda-pulumi-dev delete  — └─ aws:apigateway:x:API hello delete  — ├─ aws:apigateway:Stage hello delete  — ├─ aws:lambda:Permission hello-f61e7551 delete  — ├─ aws:apigateway:Deployment hello delete  — ├─ aws:apigateway:RestApi hello delete  — ├─ aws:iam:RolePolicyAttachment hello4c238266 delete  — ├─ aws:iam:RolePolicyAttachment hello66382ec5–32be53a2 delete  — ├─ aws:s3:BucketObject hello4c238266/index.html delete  — ├─ aws:lambda:Function hello66382ec5 delete  — ├─ aws:s3:BucketObject hello4c238266/favicon.png delete  — ├─ aws:s3:Bucket hello delete  — ├─ aws:iam:Role hello4c238266 delete  — └─ aws:iam:Role hello66382ec5 delete  Resources: — 14 to deleteDo you want to perform this destroy? yes> no details
```

Pulumi seems like a great alternative to using terraform since we can use any programming language tha we are familiar, but i found terraform docs to be far superior and with pulumi it was not as easy. This might change with more time as Pulumi is relatively new.