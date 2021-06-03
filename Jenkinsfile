
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
        stage("upload artifacts to nexus repository"){
            steps{
                echo"succes"
                
            }
        }
    }
}
