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
	sudo echo "blog updated" >> index.html
	sudo docker build -t dudwns03382/testweb:newblog .
	sudo docker push dudwns03382/testweb:newblog
	sudo echo "shop updated" >> index.html
	sudo docker build -t dudwns03382/testweb:newshop .
	sudo docker push dudwns03382/testweb:newshop
        '''
      }
    }
    stage('deploy k8s') {
      steps {
        sh '''
        sudo kauth
        sudo kubectl set image deployment deploy-main ctn-main=dudwns03382/testweb:newnewmain
	sudo kubectl set image deployment deploy-blog ctn-blog=dudwns03382/testweb:newblog
	sudo kubectl set image deployment deploy-shop ctn-shop=dudwns03382/testweb:newshop
        '''
      }
    }
  }
}

