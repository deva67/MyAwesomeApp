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
       
  }
}
