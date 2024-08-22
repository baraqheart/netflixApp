## DEVSECOPS COMPLETE PROJECT ON NETFLIXAPP
[Jenkins, sonarQube, Trivy, Javaascript, Prometheus, Grafana, Docker, Helm, Argocd and Kubernetes]
  

## 

## Install Jenkins using Docker
 - configure settings
 - install tools
   - n
 
 - install plugins
   - slack 
   - sonarqube 
 
 - create credentials for all third party apps
   - github : username and password
   - sonar : secret text
   - aws : 
   - k8s : 
   - docker: username and password 
   - slack: secret text


 - integrate with other apps
   - github : go to developer settings > create access tokens
            go to repo settings > 
   - sonarqube
   - slack: go to slack apps and search slack apps > search for jenkins and install



## Writing the Jenkins pipeline
- checkout from git
 this is where we specify the working directory to perform the workflows

- sonarqube analysis 
 [sonarqube implementation on jenkins docs](https://github.com/jenkinsci/sonarqube-plugin/blob/master/sonar-docs/analysis/scan/sonarscanner-for-jenkins.md)

Sonarqube is an open source tool used to perform code quallity check and 
to ensure code meets standards 

- quality gate
 quality gates are sets of rules and instruction to measure code quality, code smells, vulnerability check and others

 the code below, can be set to true if you want all the pipeline to fail if quality gate is not met

- install dep
  This stage install all the neccesary depencies to run the app
 
 ```
 npm install
 ```

- owasp fs 
  
- trivy fs scan
 trivy is used to check files for vulnerability

- biuld image
here we build the source code in to an image

 ```
   docker build --build-arg $(cat .env | xargs) -t $Image .
   docker tag $image $imageRegistry/$image

```

- deploy to docker
and we finally deploy to docker

- deploy to k8s
deploying to k8s

- notify slack
notification will be sent to slack 


##

##

##
