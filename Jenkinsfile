pipeline {
  agent any

  stages {
    stage("install") {
        steps {
            sh 'npm ci'
        }
    }

    stage("test") {
        steps {
            sh 'npm test'
        }
    }

    stage("build") {
        steps {
            sh 'npm run build'
        }
    }
  }
}