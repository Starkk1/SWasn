pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        script {
          bat 'dotnet build SWasn.sln'
        }
      }
    }
    stage('Docker Build') {
      steps {
        script {
          bat 'docker build -t swasn-api .'
        }
      }
    }
    stage('Deploy to Staging') {
      steps {
        script {
          bat 'docker-compose up --build -d'
        }
      }
    }
  }
}