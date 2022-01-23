## Table of contents
* [General info](#general-info)
* [Setup](#setup)

## General info

This is reusing the code publshed at https://aws.amazon.com/blogs/infrastructure-and-automation/scheduling-automatic-deletion-of-aws-cloudformation-stacks/.

There were a number of permissions for the fopr full termination of the resoruces in the t800.yaml template were missing so these have been retified and this is now working.
	
## Setup
There aqre two options to run this.

Deploy t800.yaml and in the parameters give it the name of the stack you are deploying and the time to live in minutes. 

TTL neede to be greater than 1 minute due to the time lag in deploying the stack.

The Second option is a an embeded stack, the StackName need to the the parent stack

```
Resources:
  T800:
    Type: AWS::CloudFormation::Stack
    Properties:
      TemplateURL: https://xxxxxxxxxxxx.s3.eu-west-2.amazonaws.com/t800.yml
      Parameters:
        StackName: !Ref 'AWS::StackName'
        TTL: !Ref 'TTL'
```