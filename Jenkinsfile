
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
    }
}
