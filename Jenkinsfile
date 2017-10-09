pipeline {
  agent any
  stages {
    stage('BUILD') {
      steps {
        git(url: 'https://github.com/ram-devops/mvnrepo.git', branch: 'master')
        sh 'mvn clean compile package deploy'
        sh 'export URL=`cat /var/lib/jenkins/jobs/ram-devops/jobs/final-pipe.f4038p/branches/master/builds/$BUILD_ID/log| grep Uploading |grep war | awk \'{print $2}\'`'
      }
    }
  }
}