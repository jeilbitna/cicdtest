pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/jeilbitna/cicdtest.git', branch: 'main'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        sudo docker build -t jeilbitna/cicdtest:blue .
        sudo docker push jeilbitna/cicdtest:blue
        '''
      }
    }
    stage('deploy kubernetes') {
      steps {
        sh '''
        ansible master -m command -a 'kubectl create deploy myweb3 --image=jeilbitna/cicdtest:blue'
        ansible master -m command -a 'kubectl expose deploy myweb3 --type="LoadBalancer" --port=80 --target-port=80 --protocol="TCP"'
        '''
      }
    }
  }
}
    
