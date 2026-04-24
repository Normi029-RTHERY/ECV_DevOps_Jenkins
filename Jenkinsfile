pipeline {
  agent any

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

    stage("Build") {
        steps {
            sh 'echo "Building the application..."'
        }
    }
  }
}