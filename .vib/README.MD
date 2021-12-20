VMware Image Builder content recipe for YugabyteDB. 

## Description

This folder contains the VMware Image Builder scripts for sending pipelines to VMware Image Builder and processing the resulting execution graphs. 

Here are the main contents included here:

* The [scripts](./scripts/) folder contains all the different shell utilities that interact with VMware Image Builder for submitting pipelines, checking execution status and downloading logs and reports.
* The [goss](./goss/) folder contains the server validation scripts used in Goss.
* The [chart-values](./chart-values.yaml) file contains the customizations needed for the Helm Chart. 
* [validate.json](validate.json) is the pipeline used for running linting and vulnerability scanning validation.
* **vib-xxx** scripts are the pipeline associated with the different Kubernetes platforms that are going to be tested. 

When sending a Pull Request or a Push to the master branch, a new [Github Workflow](../.github/workflows/vib.yaml) will execute. This new workflow contains all the different jobs and steps and will be reading the content in this folder and sending it to VMware Image Builder for processing. The current workflow is made of two separate jobs:

1. The first job runs the validation script and checks that the PR/Push request is linted property and does not include any severe vulnerabilities.
2. The second job runs a verification matrix on two separate platforms: GKE and AKS. For each of these platforms, three sets of tests will be executed: Goss server validation tests, resilience tests and a health check. 

For all the above, when finished either sucessfully or due to failure all the logs will be downloaded and uploaded to the Github workflow build as artifacts. 
