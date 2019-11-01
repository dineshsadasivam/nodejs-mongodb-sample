
# Sample NodeJS application with MongoDB 
--------------------------------------------------
## This example will display a web page with current page hit count as stored in persistent database.

### Create a New Project for the sample application deployment and set it as current project.
   
    $ oc new-project demoproject --display-name="Demo Project" --description="Project for demo purpose"
    $ oc project demoproject

### Pull the container images
The sample application is based on Node.JS:6 and mongodb:3.6. These container images are available in the redhat repository (registry.redhat.io). The default images in Docker do not support ppcle, hence manually pull the correct images and update into the openshift cluster repository.

 - Login to the openshift centralised repository
 
       $ docker login -u openshift -p $(oc whoami -t) docker-registry.default.svc:5000

    
 - Pull the images to the openshift cluster repository    

       $ docker pull registry.redhat.io/rhscl/mongodb-36-rhel7
       $ docker tag registry.redhat.io/rhscl/mongodb-36-rhel7 docker-registry.default.svc:5000/myproject/mongodb:3.6
       $ docker push docker-registry.default.svc:5000/myproject/mongodb:3.6
       
       $ docker pull registry.redhat.io/rhscl/nodejs-6-rhel7
       $ docker tag registry.redhat.io/rhscl/nodejs-6-rhel7 docker-registry.default.svc:5000/myproject/nodejs:6
       $ docker push docker-registry.default.svc:5000/myproject/nodejs:6

### Ensure the pre-requisite Persistent Volumes of atleast 2GiB are available
Check if PV's are available

       $ oc get pv

### Download the application template
The sample application template can be downloaded from https://github.com/dineshsadasivam/nodejs-mongodb-sample/template/nodejs-mongodb.yaml 

### Start deployment using the downloaded template
![alt text](https://raw.githubusercontent.com/dineshsadasivam/nodejs-mongodb-sample/master/pic/Import-yaml.png)


![alt text](https://raw.githubusercontent.com/dineshsadasivam/nodejs-mongodb-sample/master/pic/App-Deploy.png)

