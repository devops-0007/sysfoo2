pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'compiling sysfoo app..'
        sh 'mvn compile'
      }
    }

    stage('test') {
      parallel {
        stage('test') {
          steps {
            echo 'running unit tests...'
            sh 'mvn clean test'
          }
        }

        stage('SCA') {
          steps {
            sleep 4
          }
        }

        stage('SBOM') {
          steps {
            sleep 2
          }
        }

      }
    }

    stage('package') {
      steps {
        echo 'package the artifact...'
        sh 'mvn package -DskipTests'
        archiveArtifacts 'target/*.jar'
      }
    }

  }
  tools {
    maven 'Maven 3.6.3'
  }
  post {
    always {
      echo 'This pipeline is completed..'
    }

  }
}