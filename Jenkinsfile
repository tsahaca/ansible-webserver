pipeline {
  agent {label "agentfarm"}
  stages {
    stage('Delete the workspace') {
      steps {
        deleteDir()
      }
    }
    stage('Installing Ansible') {
      steps {
        script{
          def ansible_exists = fileExists '/usr/bin/ansible'

          if(ansible_exists){
            echo "Skipping ansible install - alreday exists"
          } else {
            sh 'sudo apt-get update -y && sudo apt-get upgrade -y'
            sh 'sudo apt install -y wget tree unzip ansible python3-pip python-apt'
          }
        }
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