pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/YoonHakyoung/cicdtest.git', branch: 'main'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        sudo docker build -t yoonhakyoung/cicdtest:1.0 .
        sudo docker push yoonhakyoung/cicdtest:1.0
        '''
      }
    }
    stage('deploy kubernetes') {
      steps {
        sh '''
        ansible master -m command -a 'kubectl create deployment pl-bulk-prod --image=yoonhakyoung/cicdtest:1.0'
        ansible master -m command -a 'kubectl expose deployment pl-bulk-prod --type=LoadBalancer --port=80 --target-port=80 --name=pl-bulk-prod-svc'
        '''
      }
    }
  }
}
