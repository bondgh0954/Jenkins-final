# Jenkins-final
# Project Description

   Configure webserver on digitalOcean and run jenkins on it
   Create multibranch pipeline
   pipeline 
   dynamically increment application version
   build jar application
   build applicatioin into docker image 
   push image into private docker registry
   pull image from the registry and deploy it on aws ec2 instance
   commit version increment changes into the source code management(git)
  
  

# Technologies used
  Jenkins
  Docker
  AWS EC2
  Digital Ocean
  git
# Detailed project Description
## Step 1
  Create and configure a server on digialOcean
  Set firewall configuration to open port 8080 for jenkins container and install docker on the server
  run jenkins docker image container on the server
       docker run -p 8080:8080 -p 50000:50000 -d jenkins_home:/var/jenkins_home jenkins/jenkins:lts
       

