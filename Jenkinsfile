pipeline {
  agent any
  stages {
    stage('SCM') {
      steps {
        git(credentialsId: '7fc12b07-029e-4622-8d84-c7001d5a90b6', url: 'https://github.com/Indhumathi697/gitrepo2', branch: 'main')
      }
    }

    stage('Build&Publish') {
      steps {
        sh '''sudo docker build -t indhumathi926/srepo1:latest .
sudo docker push indhumathi926/srepo1:latest'''
      }
    }

    stage('Deploy') {
      parallel {
        stage('DeployDev') {
          steps {
            sh '''sudo docker rm -f $(sudo docker ps -aq)||true
sudo docker run -d -p 7777:80 --name devcon1 indhumathi926/srepo1:latest'''
          }
        }

        stage('DeployQA') {
          steps {
            sh '''sudo docker rm -f $(sudo docker ps -aq)||true
sudo docker run -d -p 9999:80 --name qacon1 indhumathi926/srepo1:latest'''
          }
        }

      }
    }

  }
}