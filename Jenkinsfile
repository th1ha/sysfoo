pipeline {
  agent any

  tools {
    // # manage jenkins>tools>maven
    maven 'maven - 3.9.11' 
  }

  stages {
    stage('build_job') {
      steps {
        echo "building app"
        sh 'mvn compile'
      }
    }

    stage('test_job') {
      steps {
        echo "running unit tests"
        sh 'mvn clean test'
      }
    }

    stage('package_job') {
      steps {
        echo "packaging app"
        sh 'mvn package -DskipTests'
      }
    }
  }

  post {
    always {
      echo "Pipeline is completed"
    }
  }
}