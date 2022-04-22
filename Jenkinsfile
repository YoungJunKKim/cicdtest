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
	sudo sed -i 's/<h2> UPDATED MAIN PAGE </h2>/<h2> UPDATED BLOG PAGE </h2>/g' index.html
	sudo docker build -t dudwns03382/testweb:newnewblog .
	sudo docker push dudwns03382/testweb:newnewblog
	sudo sed -i 's/<h2> UPDATED BLOG PAGE </h2>/<h2> UPDATED SHOP PAGE </h2>
/g' index.html
	sudo docker build -t dudwns03382/testweb:newnewshop .
	sudo docker push dudwns03382/testweb:newnewshop
        '''
      }
    }
    stage('deploy k8s') {
      steps {
        sh '''
        sudo kauth
        sudo kubectl set image deployment deploy-main ctn-main=dudwns03382/testweb:newnewmain
	sudo kubectl set image deployment deploy-blog ctn-blog=dudwns03382/testweb:newnewblog
	sudo kubectl set image deployment deploy-shop ctn-shop=dudwns03382/testweb:newnewshop
        '''
      }
    }
  }
}

