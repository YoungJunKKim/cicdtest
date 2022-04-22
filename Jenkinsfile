pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/YoungJunKKim/cicdtest.git', branch: 'master'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        sudo docker build -t dudwns03382/testweb:newnewmain .
        sudo docker push dudwns03382/testweb:newnewmain
        '''
      }
    }
    stage('deploy k8s') {
      steps {
        sh '''
        sudo kauth
        sudo kubectl set image deployment deploy-main ctn-main=dudwns03382/testweb:newnewmain
        '''
      }
    }
  }
}

