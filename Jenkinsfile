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
    stage ('Nexus Upload') {
      steps {
      nexusArtifactUploader(
      nexusVersion: 'nexus3',
      protocol: 'http',
      nexusUrl: 'ec2-18-116-32-17.us-east-2.compute.amazonaws.com:8081',
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
      }
    stage ('DEV Deploy') {
      steps {
      echo "deploying to DEV Env "
      deploy adapters: [tomcat9(credentialsId: 'a7f0f3a8-16b5-4c98-918b-ff44789c583b', path: '', url: 'http://ec2-3-145-196-2.us-east-2.compute.amazonaws.com:8090/')], contextPath: null, war: '**/*.war'
      }
    }
    stage ('Slack Dev Notification') {
      steps {
        echo "deployed to DEV Env successfully"
        slackSend(channel:'myappfeb', message: "Job is successful, here is the info -  Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
      }
    }
  }
  }
