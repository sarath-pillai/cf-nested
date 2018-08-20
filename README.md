# AWS Cloudformation Nested Stacks

As your infrastructure grows, common patterns can emerge in which you declare the same components in multiple templates. You can separate out these common components and create dedicated templates for them. Then use the resource in your template to reference other templates, creating nested stacks.

This example repo uses main.yaml file to trigger other stacks from templates/ directory. 

# How Does main.yaml call other stacks

Main.yaml uses a list of Resources in yaml format, with any resouce name that can be referenced beneath, with TemplateURL parameter pointing to the location in s3, where template directory contents for that particular resource is available. 
```sh
Resources:
    VPC:
        Type: AWS::CloudFormation::Stack
        Properties:
            TemplateURL: https://s3.amazonaws.com/sarath-cf-nested/templates/vpc.yaml
            Parameters:
                Environment:        !Ref AWS::StackName

    SecurityGroups:
        Type: AWS::CloudFormation::Stack
        Properties:
            TemplateURL: https://s3.amazonaws.com/sarath-cf-nested/templates/security-group.yaml
            Parameters: 
```
