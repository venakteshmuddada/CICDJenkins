pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/venakteshmuddada/CICDJenkins.git'
      }
    }

    stage('Build') {
      steps {
        echo 'Building app...'
        sh 'echo Simulate Maven/Gradle/NPM Build'
      }
    }

    stage('Docker Build & Run') {
      steps {
        script {
          sh '''
            docker build -t my-app .
            docker stop my-app || true
            docker rm my-app || true
            docker run -d -p 80:3000 --name my-app my-app
          '''
        }
      }
    }
  }
}
