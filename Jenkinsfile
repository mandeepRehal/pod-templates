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
          label 'nodejs-pod'
          yamlFile 'linux/nodejs-pod.yaml'
        }
      }
      steps {
        checkout scm
        container('nodejs') {
          echo 'Hello World!'   
          sh 'node --version'
          sleep 30
        }
      }
    }
    stage('Test-windows') {
      agent {
        kubernetes {
//        label from UI
//        label 'windows-test'
	  label 'windows-pod'
          yamlFile 'windows/dotnet-pod.yaml'
        }
      }
      steps {
	sleep 30
        bat 'dir'
//       container(name:'windows-sdk'){
//        bat 'dotnet -h'
//       } 
     }
    }
  }
}
