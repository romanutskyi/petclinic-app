pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
              echo '=== Building Petclinic Docker Image ==='
              script {
                  sh 'git pull origin master'
                  app = docker.build("romanutskyi/petclinic-app")
                  }
              }
        }
        stage('Push') {
            steps {
            echo '=== Pushing Petclinic Docker Image To DockerHub Registry==='
              script {
                  docker.withRegistry('https://registry.hub.docker.com', '${DOCKER_CREDS}') {
                      app.push("$BUILD_NUMBER")
                      app.push("latest")
                      }
              }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
