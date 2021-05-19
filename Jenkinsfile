
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
                script{
                    def pom = readMavenPom file: 'pom.xml'
                    def repository = pom.version.endswith("SNAPSHOT") ? 'pnkr5454_snapshot' : 'pnkr5454_release'
                    nexusArtifactUploader artifacts: 
                    [[artifactId: 'myweb', 
                    classifier: '', 
                    file: "target/myweb-${pom.version}.war", 
                    type: 'war']], 
                    credentialsId: 'Nexus3', 
                    groupId: 'in.javahome', 
                    nexusUrl: '172.31.3.30:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: repository,
                    version: pom.version
                }
                
            }
        }
    }
}
