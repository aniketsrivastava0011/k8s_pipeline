# aws pipeline deploying eks pods
This repository contains sample codes to work with AWS Codepipeline, ECR, EKS, IAM and Codebuild
This is a node.js project, but add config as per your project requirement 

#Pre-Requisite for pipeline
-Create an AWS EKS cluster with required nodes/nodegroup.
-Initiate communication with your CLI 
-Edit aws-auth and add arn of service role created for AWS CodeBuild.
-Initiate a load balancer service on cluster so that output can be checked.
-Create a simple AWS CodePipeline and AWS CodeBuild project.
 
# eks folder
Files in eks folder can be used for further configuration in eks cluster.
1. aws-auth.yml - for configmap
2. create_iam_role.sh - to create service role for AWS CodeBuild.
3. deployment.yaml - for using newer docker image from registry.
4. service.yaml - to start a load balancing service inside cluster.
5. prereqs.sh - to get an idea what utilities system should have or can be use in pre-build stage as a fair parallel check.

# Dockerfile
Used get packages, npm install and exposing port. Whithout this build will not be possible.

#eks.yml
This is buildspec.yml for my case. Having the stages:

1. install - removing previous kubectl version available on build server/platform and installing required version of kubectl.
2. pre-build - configuring build server/platform for operation ready. Configuring .kube/config file (having all the cluster information) and docker registry connection.
3. build - the Dockerfile will fetch all the node dependencies, packages and app bundle into the new pulled image conditional environment.
4. post-build - image will be build and pushed to registry and new changes on service will be rolled out.
 


