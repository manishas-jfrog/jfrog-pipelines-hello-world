# jfrog-pipelines-hello-world

This is a simple, "hello world" level example that defines a pipeline with 3 linear steps, triggered by a Github repository.

![alt text](https://github.com/manishas-jfrog/jfrog-pipelines-hello-world/blob/master/images/hello-world-pipeline-image.png "JFrog Pipelines Hello world")

Pre-requisites:

- [JFrog Pipelines installed](https://www.jfrog.com/confluence/display/CICD/Installing+JFrog+Pipelines) (needs Artifactory 6.11 or above)
- User account created in Artifactory with deploy permissions to at least one binary repository  

Steps to run this pipeline:

- Fork this repository to your Github account
- Sign in to JFrog Pipelines with your Artifactory credentials
- Follow instructions to [add an integration](https://www.jfrog.com/confluence/display/CICD/Adding+Integrations) and create a [Github integration](https://www.jfrog.com/confluence/display/CICD/GitHub+Integration) to connect Github to Pipelines
- Edit the config file `jfrog-pipelines-hello-world.yml` in your fork of this repo and replace the following in the GitRepo resource:
    - gitProvider should point to your Github integration
    - path should point to your fork of this repository
  Save and commit the yaml file.  
- [Add a pipeline source](https://www.jfrog.com/confluence/display/CICD/Adding+a+Pipeline+Source) and point it to the `jfrog-pipelines-hello-world.yml` in your fork of this repo. This adds your configuration to the platform and a pipeline is created based on your YAML. At this point, you can go to the **View Pipelines** page and see a pipeline with the structure as shown in the screenshot above.
- You can now commit to the repo to trigger your pipeline, or trigger it manually through the UI.

This pipeline demonstrates the following:

- Defining a [GitRepo resource](https://www.jfrog.com/confluence/display/CICD/GitRepo), which acts as the trigger for the pipeline. When this resource is created, the platform automatically adds webhooks to the source control repository with the specified configuration.
- Defining a [Bash step](https://www.jfrog.com/confluence/display/CICD/Bash), which lets you execute any commands you need for your automation.
- Defining `inputResources` and `inputSteps` to create a workflow
- Using environment variables (e.g. $res_someRepo_commitSha) to extract information from `inputResources`
- Using utility functions for state mgmt (e.g. add_run_variables first_stepid=$step_id) to exchange information across steps

