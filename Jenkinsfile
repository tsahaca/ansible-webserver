pipeline {
  agent {label "agentfarm"}
  stages {
    stage('Delete the workspace') {
      steps {
        deleteDir()
      }
    }
    stage('Second Stage') {
      steps {
        echo "Second stage"
      }
    }
    stage('Third Stage') {
      steps {
        echo "Third stage"
      }
    }
  }
}