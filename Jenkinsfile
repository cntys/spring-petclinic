pipeline {
  agent none
  stages {
    stage('Maven Install') {
      agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
      }
      steps {
        sh 'mvn -B -DskipTests clean package'
      }
    }
    stage('Docker Build') {
      agent any
      steps {
        sh 'docker build -t testtys/spring-petclinic:latest .'
      }
    }

    stage('Docker Push') {
      agent any
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerHubAccount', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "docker login -u ${dockerHubUser} -p ${dockerHubPassword}"
          sh 'docker push testtys/spring-petclinic:latest'
        }
      }
    }

    stage('Pull Image'){
        agent any
        steps{
            sh "docker pull testtys/spring-petclinic:latest"
            sh 'docker run -d --rm -p 18081:8080 --name spring-petclinic testtys/spring-petclinic:latest'
        }

    }
  }
}