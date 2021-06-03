
pipeline{
    agent any
    tools{
        maven 'maven1'
    }
    stages{
        stage("build the artifacts by maven"){
            steps{
                sh "mvn clean package"
            }
        }
        stage("build the docker image"){
            steps{
                sh"docker build -t pnkr5454/myapp2021:v1 ."
                
            }
        }
          stage("push docker image to docker hub"){
            steps{
                withCredentials([string(credentialsId: 'docker_pswd', variable: 'docker_hub')]){
                sh"docker login -u pnkr5454 -p ${docker_hub}"
                sh"docker push pnkr5454/myapp2021:v1"
                }
            }
        }
        stage("pull the image and deploy to tomcat"){
            steps{
                sshagent(['docker_hub']) {
                sh"ssh ec2-user@172.31.94.70 docker run -d -p 8080:8080 pnkr5454/myapp2021:v1 "
                 } 
            }
        }
    }
}
