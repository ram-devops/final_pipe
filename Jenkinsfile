pipeline {
  agent any
  stages {
    stage('BUILD') {
      steps {
        git(url: 'https://github.com/ram-devops/mvnrepo.git', branch: 'master')
        sh 'mvn clean compile package deploy'
        sh '''pwd

ls'''
      }
    }
  }
}