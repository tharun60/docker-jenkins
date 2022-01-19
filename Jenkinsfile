pipeline {
  agent any
  tools {
    maven 'mvn-3.8.4'
  }

  stages {
       
    stage('Maven Install') {
    /*  agent {
        docker {
          image 'maven:3.5.0'
        }
      } */
      steps {
        sh 'mvn clean install'
      }
    }
    stage('Docker Build') {
      agent any
      steps {
        sh 'docker build -t tharun60/dockersample:2 .'
      }
    }
    stage('Docker Push') {
      agent any
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh 'docker push tharun60/dockersample:2'
        }
      }
    }
  }
}
