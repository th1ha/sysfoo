pipeline {
  agent any
  stages {
    stage('build_job') {
      steps {
        echo 'building app'
        sh 'mvn compile'
      }
    }

    stage('test_job') {
      steps {
        echo 'running unit tests'
        sh 'mvn clean test'
      }
    }

    stage('package_job') {
      steps {
        echo 'packaging app'
        sh '''# Truncate the GIT_COMMIT to the first 7 characters
GIT_SHORT_COMMIT=$(echo $GIT_COMMIT | cut -c 1-7)
# Set the version using Maven
mvn versions:set -DnewVersion="$GIT_SHORT_COMMIT"
mvn versions:commit'''
        sh 'mvn package -DskipTests'
        archiveArtifacts '**/target/*.jar'
      }
    }

  }
  tools {
    maven 'maven - 3.9.11'
  }
  post {
    always {
      echo 'Pipeline is completed'
    }

  }
}