pipeline {
  agent any

  stages {
    stage('Prepare / Check') {
      steps {
        echo "Checking Docker and Compose availability"
        sh 'docker --version || true'
        sh 'docker compose version || docker-compose version || true'
      }
    }

    stage('Checkout') {
      steps {
        // checkout the same repo that contains this Jenkinsfile
        checkout scm
      }
    }

    stage('Build Docker Images') {
      steps {
        // build images defined in docker-compose.yml
        sh 'docker compose build --pull --parallel'
      }
    }

    stage('Login & Push to Docker Hub') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
          sh '''
            echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
            docker compose push
            docker logout || true
          '''
        }
      }
    }

    stage('Deploy (Docker Compose)') {
      steps {
        sh '''
          # safe deploy sequence
          docker compose down || true
          docker compose pull || true
          docker compose up -d
        '''
      }
    }
  }

  post {
    always {
      echo 'Pipeline finished'
    }
  }
}
