pipeline {
  agent any
  stages {
    stage('buzz build') {
      steps {
        echo 'starting build'
        sh '        ./jenkins/build.sh'
        archiveArtifacts(artifacts: 'target/*.jar', fingerprint: true)
      }
    }
    stage('buzz test') {
      parallel {
        stage('testing a') {
          steps {
            echo 'starting test'
            sh './jenkins/test-all.sh'
            junit '**/surefire-reports/**/*.xml'
          }
        }
        stage('testing b') {
          steps {
            sh '''sleep 10
echo done.'''
          }
        }
      }
    }
  }
  environment {
    BUZZ_NAME = 'Worker Bee'
  }
}