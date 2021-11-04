## CI/CD Pipeline with azure devops 
Configure CI/CD pipelines to deploy the Node Weight Tracker application for 2 environments: Staging and Production. </br>
### The goal:
![image](https://user-images.githubusercontent.com/71599740/140197294-11143f63-c432-4c57-b5b7-13827e8c9075.png)

### Welcome To azure devops!
![image](https://user-images.githubusercontent.com/47865329/140266113-883ef7b7-1662-42dd-adbb-549ddab668b3.png)


There are 2 pipelines:
CI pipeline - creating an artifact and uploading to Artifactory
CD Pipeline - Downloading the LTS artifact from artifactory and running the new app.

## STEPS:
* Configure an agent: [agent-pool](https://www.youtube.com/watch?v=psa8xfJ0-zI&ab_channel=Raaviblog)
* Run the agent as a systemd service: [service](https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/v2-linux?view=azure-devops)
* Import a project repository [Weight Tracker](https://github.com/orel199973/bootcamp-app)
* Create a new artifacts feed
* Created the build pipeline using the visual editor
* Selected the imported repository as build sources - GITHUB
* Selected the "Empty Job" template
* Configured the pipeline to run in the agent-pool (CI)
* Configure CI Trigger: Enable continuous integration   => If you would like to make a change to the app push the new commit to the master branch and the pipelines will do the rest
* Create these tasks:
![image](https://user-images.githubusercontent.com/47865329/140266466-64e7ac10-20ff-424a-ba25-0e861db04d13.png)
![image](https://user-images.githubusercontent.com/47865329/140266531-16bbeb19-73c1-464a-aa86-22b9517be82d.png)
![image](https://user-images.githubusercontent.com/47865329/140266605-50d39769-f86c-4dfd-9793-594cf197bbba.png)
* Click on "add a new artifact" and add [ansible-repo](https://github.com/orel199973/CI_CD_Ansible)
![image](https://user-images.githubusercontent.com/71599740/140198353-9679236a-b805-499f-af56-4ef1bdc9b96b.png)
![image](https://user-images.githubusercontent.com/47865329/140267142-ea4b6f71-ccc4-4b02-8e8e-19f6c94394bc.png)
* Create a release pipeline definition -Click on "add a new artifact"
* Configure the artifact trigger: Continuous deployment trigger: Enabled
* Create a file creator that set the variables by the correct group - staging / prod
![image](https://user-images.githubusercontent.com/47865329/140267436-7fedf9e8-ef90-428b-87b5-d1ff5b65179b.png)
* Create the group variables and edit them: ![image](https://user-images.githubusercontent.com/47865329/140267713-ac3dfaa1-0e74-45aa-88a6-c9a7d9b4f87e.png)
* Copy the application artifact to the remote machines (vm-staging1 and vm-staging2)
![image](https://user-images.githubusercontent.com/47865329/140267889-20a34a78-ac19-4f48-9a65-82fa531d30bd.png)
* Then run the playbook:
![image](https://user-images.githubusercontent.com/71599740/140199003-be1d5eea-43b3-4215-88c1-2db241863fe2.png)
![image](https://user-images.githubusercontent.com/71599740/140199039-69846f1a-7eb9-47f6-9cc9-f17c9c38ae5f.png)

* finally this is the full ci-cd:
![image](https://user-images.githubusercontent.com/47865329/140268293-c2e087f2-5952-47bd-aa9f-807989337dbe.png)


![image](https://user-images.githubusercontent.com/47865329/140268431-a2f97e81-7e8a-4999-88fc-1f7b2a7e65ad.png)
![image](https://user-images.githubusercontent.com/47865329/140268487-70c0beba-01d1-4ff5-aa75-7cd80775fb2c.png)


If you would like to make a change to the app push the new commit to the master branch and the pipelines will do the rest :)


# Emphasis:
* To provision the infrastructure I've used my previous project: https://github.com/orel199973/CI_CD_Ansible
* To install all dependencies on the nodes and to deploy and run the application for the first time I've used this project: https://github.com/orel199973/bootcamp-app
* The terraform repo: https://github.com/orel199973/CI_CD_Terraform
