rtMaven = null
server= null
pipeline {
  agent any
  tools {
    maven 'Maven3'
  }
  stages {
    stage ('Build') {
      steps {
      sh 'mvn clean install -f MyWebApp/pom.xml'
      }
    }
    stage ('JaCoCo') {
      steps {
      jacoco()
      }
    }
    
     stage ('Nexus upload')  {
     steps {
        nexusArtifactUploader(
        nexusVersion: 'nexus3',
        protocol: 'http',
        nexusUrl: 'http://ec2-18-116-32-17.us-east-2.compute.amazonaws.com:8081',
        groupId: 'myGroupId',
        version: '1.0-SNAPSHOT',
        repository: 'maven-snapshots',
        credentialsId: '2e8c8ad0-924e-4364-8937-ad2b83d04511',
        artifacts: [
            [artifactId: 'MyWebApp',
             classifier: '',
             file: 'MyWebApp/target/MyWebApp.war',
             type: 'war']
        ])
         }
    )
    
  }
}
