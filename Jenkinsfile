
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
                    def repository = pom.version.endsWith("SNAPSHOT") ? 'pnkr5454_snapshot' : 'pnkr5454_release'
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
        stage("download artifacts from nexus repository"){
            steps{
                sh "curl -u admin:Malleswari@4343 -L -X GET "http://3.91.174.181:8081/service/rest/v1/search/assets/download?sort=version&repository=pnkr5454_release&maven.groupId=in.javahome&maven.artifactId=myweb&maven.extension=war" -H "accept: application/json" -o myweb.war"
            }
        }
    }
}
