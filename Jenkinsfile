pipeline {
  agent none
  stages {
    stage('Maven Install') {
      agent {
        docker {
          image 'maven:3-alpine'
        }
      }
      steps {
        sh 'mvn clean install'
      }
    } 
  }
}