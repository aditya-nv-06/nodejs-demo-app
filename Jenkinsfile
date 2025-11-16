pipeline {
  agent any
  environment {
    DOCKER_IMAGE = "aditya-nv-06/nodejs-demo-app:latest"
    DOCKER_REGISTRY = "docker.io" // e.g., "docker.io/aditya-nv-06"
  }
  stages {
    stage("build") {
      steps {
        echo "Building"
        // NodeJS build commands, e.g., npm install
        sh 'npm install'
      }
    }
    stage("start") {
      steps {
        echo "starting"
        // NodeJS test commands, e.g., npm test
        sh 'npm run start'
      }
    }
    stage("docker build") {
      steps {
        echo "Building Docker image"
        sh "docker build -t $DOCKER_IMAGE ."
      }
    }
    stage("docker push") {
      steps {
        echo "Pushing Docker image"
        withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
          sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin $DOCKER_REGISTRY"
          sh "docker push $DOCKER_IMAGE"
          sh "docker logout $DOCKER_REGISTRY"
        }
      }
    }
  }
}
