pipeline {
    agent any
    environment{
        DOCKER_TAG = getDockerTag()
        INSTANCE_IP = getInstanceIp()
    }
    stages{
        stage('Build Docker image'){
           steps{
              sh "docker build . -t raghavendrachervirala/pentagon:${DOCKER_TAG}"
           }
        }
        stage('Dockerhub push'){
          steps{
            withCredentials([string(credentialsId: 'docker-hub', variable: 'dockerHubPwd')]) {
                 sh "docker login -u raghavendrachervirala -p ${dockerHubPwd}"
                 sh "docker push raghavendrachervirala/pentagon:${DOCKER_TAG}"
            }
          }
        }
    }
}

def getDockerTag(){
   def tag = sh script: 'git rev-parse HEAD', returnStdout: true
   return tag
}

def getInstanceIp(){
   def ip = sh script: 'curl ifconfig.co', returnStdout: true
   return ip;
}
