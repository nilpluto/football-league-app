pipeline {
  agent any

    environment {
        DOCKER_HUB_LOGIN = credentials('docker-hub')
    }

  triggers {
    pollSCM('* * * * *')
  }

  stages {
      stage('Build') {
          steps {
              sh './gradlew assemble'
          }
      }
      stage('Test') {
          steps {
              sh './gradlew test'
          }
      }
      stage('Build Docker image') {
          steps {
              sh './gradlew docker'
          }
      }

      stage ('Build & Push docker image') {
          steps {
              withDockerRegistry(credentialsId: DOCKER_HUB_LOGIN, url: 'https://hub.docker.com/') {
                  sh 'docker push justacoder7/football-league-app'
              }
          }
      }

//       stage('Push Docker image') {
//           environment {
//               DOCKER_HUB_LOGIN = credentials('docker-hub')
//           }
//           steps {
//               sh 'docker login --username=$DOCKER_HUB_LOGIN_USR --password=$DOCKER_HUB_LOGIN_PSW'
//               sh './gradlew dockerPush'
//           }
//       }
  }
}