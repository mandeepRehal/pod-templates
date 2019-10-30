pipeline {
  agent none
  options { 
    buildDiscarder(logRotator(numToKeepStr: '2'))
    skipDefaultCheckout true
  }
  stages {
    stage('Test-linux') {
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
        }
      }
    }
    stage('Test-windows') {
      agent {
        kubernetes {
	  label 'windows-pod'
          yamlFile 'windows/dotnet-pod.yaml'
        }
      }
      steps {
        bat 'dir'
//        container(name:'windows-dotnet'){
//          bat 'dotnet -h'
//      } 
     }
    }
  }
}
