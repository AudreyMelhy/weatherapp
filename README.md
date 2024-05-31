1- get the code url from the version control -----> Ask the dev team
2- as the developper for any extra specifications -----> Ask the dev team
3- determine the number of service ---> UI, weather, auth, redis, db ( 5 services)
4- determine the number of service develop by my company  -----> Ask the dev team UI, weather, auth (3 services)
5  determine the number of  third party service NOT develop by my company -----> redis, db ( 2 services)
6- make sure I have all the dockerfile for the services my compay has developed  -----> verified 

7- write the dockerfile for  third party service NOT develop by my company -----> write Dockerfile for redis and db ( 2 services) ##


8- determine with devops team the deployment strategy  ----->  Docker-compose

9 - make sure all required file for the deployment strategy is available -----> verified 

10 - determine how to manage secrets (very important) ----> count secrets(3) secret will be manage by jenkins secret store

11- determine all deployment stages involve 
     * write the Jenkinsfile 
       CODE
          * clone the code  ---->  setup  a webhook
          * check important file if required  ----> sonarqube property file required
          * build code binary if required   language ( Node, go, python )
       CODE SCANNING
        * scan the code using sonar-scanner  ----> check sonar-scanner --> jenkins ---->  sonarqube connection
        * report to sonarqube UI         ---->  sonarqube, jenkins connection
       CODE QUALITY
        * check quality gate 
             *  if the code PASS build continue  ---->  incorprate quality gate in jenkinsfile
             *  if the code FAILS  build STOP


################# if CODE QUALITY pass #########################
       BUILD DOCKER IMAGES
       
            * build images using docker   ---->  happen in all branches
       PUSH  DOCKER IMAGES TO DOCKERHUB
              * if the commit branch is NOT  develop
                  * DO NOT PUSH    ---->    not a Pull Request
              * if the commit branch is  develop
                  * PUSH to dockerhub   ----> if Pull Request
        ############## if the commit branch is  develop  ######################### ----> if Pull Request
                      * deploy the application 
                           * contruct the docker-compose  ----> EOF 
                           * deploy to a VM ----> Jenkins to launch the VM
                                       PS: this instance cannot be controled by jenkins and 
                                            cannot not be a dynamic agent for jenkins but a static agent instead.
        SMOCK CHECK
            * smock check of the application after deployment -------> query the application header
        POST BUILD 
            * notify devops team on build output  on slack     -----> jenkins ----> slack ----> end user
            

12 - create the project Jenkins 
13 - make all required connection ---------> plugin etc  
14- implement the project in jenkins  

