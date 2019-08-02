pipeline {
  agent none
  options { 
    buildDiscarder(logRotator(numToKeepStr: '2'))
    skipDefaultCheckout true
  }
  stages {
    stage('Test-node') {
      agent {
        kubernetes {
          label 'nodejs-app-pod'
          yamlFile 'lin-node/nodejs-pod.yaml'
        }
      }
      steps {
        checkout scm
        container('nodejs') {
          echo 'Hello World!'   
          sh 'node --version'
        }
      }
    }
    stage('Test-windows') {
      agent {
        kubernetes {
          label 'windows-test'
//          yamlFile 'win/win-pod.yaml'
        }
      }
      steps {
        checkout scm
        bat 'dir'
      }
    }
  }
}
