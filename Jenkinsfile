pipeline {
  agent any
  stages {
    stage('BUILD') {
      steps {
        git(url: 'https://github.com/ram-devops/mvnrepo.git', branch: 'master')
        sh 'mvn clean compile package deploy'
        sh 'echo URL=`cat /var/lib/jenkins/jobs/ram-devops/jobs/final-pipe.f4038p/branches/master/builds/$BUILD_ID/log| grep Uploading |grep war | awk \'{print $2}\'`>/tmp/env'
      }
    }
    stage('Deploy DEV') {
      steps {
        build 'rundeck_input'
      }
    }
    stage('QA') {
      steps {
        sh '''curl -s http://35.193.100.76:8080/student/ |grep "First Name"
if [ $? -ne 0 ]; then
exit 1
fi
'''
      }
    }
    stage('Approval') {
      steps {
        emailext(subject: 'Need Approval', body: '$BUILD_URL', to: 'root@localhost')
      }
    }
  }
}