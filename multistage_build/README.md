# MULTISTAGE BUILD 
#### Docker container pipelines 

The application we are using as a POC can be downloaded from:  https://github.com/rmotr/flask-api-example

##### Running tests and validation in the applicaiton


We are going to build this application inside a docker container and run:
1. Code analysis
2. Unit tests
3. SonarQube for security check


NOTE:
    - you must creat a local network on wich the test will run 
$ docker network create (custom neme)
    - you must have the sonarqube service running before runnig the pipeline file
$ docker run -d --network (custom network name) --rm --name sonarqube -p 0.0.0.0:9000:9000 sonarqube
    or as an alternative you can run the yaml file
$ docker-compose up -d 
    * make sure to note the service name and the network inside the file
    
- Reasure the linting files are correct by choosing the fixed file or fix it manually in (dir:/flask-api/api/_05_flask_restful_simple)
- once your sonarqube is running on (localhost:9000) you`d be asked to change the password 
    * default: usr:admin paswd:admin 
! make the according changes -> sonar-runner.properties file (config)

- add 127.0.0.1.nip.io to your local /etc/hosts file. 

Now you`r ready to go: 
$ docker build --network nexus_nexus -t 127.0.0.1.nip.io/multistage:v1 -f Dockerfile-pipelines .

in case you receive a buildkit error add DOCKER_BUILDKIT=0 to the command prefix:
$ DOCKER_BUILDKIT=0 docker build --network nexus_nexus -t 127.0.0.1.nip.io/multistage:v1 -f Dockerfile-pipelines .






