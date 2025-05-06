pipeline {
  agent any

  environment {
    DOCKER_IMAGE = 'my-java-app'
    CONTAINER_NAME = 'java-app-container'
    PORT = '8080'
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/venakteshmuddada/CICDJenkins.git'
      }
    }

    stage('Build with Maven') {
      steps {
        echo 'Building Java app using Maven...'
        sh 'mvn clean package'
      }
    }

    stage('Docker Build & Run') {
      steps {
        script {
          echo 'Building Docker image and starting container...'
          sh '''
            docker build -t $DOCKER_IMAGE .
            docker stop $CONTAINER_NAME || true
            docker rm $CONTAINER_NAME || true
            docker run -d -p 80:$PORT --name $CONTAINER_NAME $DOCKER_IMAGE
          '''
        }
      }
    }
  }
}
