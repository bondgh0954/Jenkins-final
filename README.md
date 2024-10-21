# Jenkins-final
# Project Description

   Configure webserver on digitalOcean and run jenkins on it <br/>
   Create multibranch pipeline <br/>
   pipeline <br/>
   dynamically increment application version <br/>
   build jar application <br/>
   build applicatioin into docker image <br/>
   push image into private docker registry <br/>
   pull image from the registry and deploy it on aws ec2 instance <br/>
   commit version increment changes into the source code management(git) <br/>
  
  

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
       

