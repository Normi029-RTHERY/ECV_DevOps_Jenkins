pipeline {
  agent any

  options {
    disableConcurrentBuilds() // interdit le fait de pouvoir lancer ce job plusieurs fois en même temps, évite les conflits d'accès aux ressources partagées
    parallelAlwaysFailFast() // si une des branches d'un bloc parallel échoue, les autres branches sont arrêtées immédiatement
  }

  environment {
    IMAGE_NAME = 'jenkins-nodeapp'
  }

  stages {
    stage("Install") {
        steps {
            sh 'npm ci'
        }
    }

    stage("Linting et Tests") {
        parallel {
            stage("Lint") {
                steps {
                    sh 'npm run lint'
                }
            }
            stage("Tests") {
                steps {
                    sh 'npm run test:coverage'
                }
            }
        }
    }

    stage("Build Image") {
        steps {
            sh '''
            docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} .
            docker tag ${IMAGE_NAME}:${BUILD_NUMBER} ${IMAGE_NAME}:latest
            '''
        }
    }

    stage("Deploy"){
      steps {
        sh 'docker run -d ${IMAGE_NAME}:${BUILD_NUMBER} -p 3000:3000 --name ${IMAGE_NAME}_${BUILD_NUMBER}'
      }
    }
  }
}