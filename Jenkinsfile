pipeline {
  agent any
  stages {

    stage('Initialize'){
        

        steps{
            def dockerHome = tool 'myDocker'
            def mavenHome  = tool 'myMaven'
            env.PATH = "${mavenHome}/bin:${env.PATH}"

            echo env.PATH

        }
    }

    stage('Checkout') {
        
        steps{
            checkout scm
        }
    }

    stage('Build'){
        
        steps{
            sh "mvn clean install"
        }
    }

    stage('Docker Build') {
      
      steps {
        sh 'docker build -t shanem/spring-petclinic:latest .'
      }
    }

  }
}