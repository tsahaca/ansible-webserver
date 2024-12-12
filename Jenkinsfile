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
    stage('Checkout Ansible Webserver Code') {
      steps {
        git branch: 'main', credentialsId: 'git-repo-creds', url: 'git@github.com:tsahaca/ansible-webserver.git'
      }
    }
    
    stage('Run ansible-lint against playbook') {
      steps {
        sh 'docker run --rm -v $WORKSPACE/playbooks:/data cytopia/ansible-lint:4 apache-install.yml'
        sh 'docker run --rm -v $WORKSPACE/playbooks:/data cytopia/ansible-lint:4 website-update.yml'
        sh 'docker run --rm -v $WORKSPACE/playbooks:/data cytopia/ansible-lint:4 website-test.yml'

      }
    }

    stage('Send Slack Notification'){
          steps{
                slackSend color: 'warning', message: "Mr. Deeds: Please approve ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.JOB_URL}) | Open)"
          }
        }
        
    stage('Request Input'){
          steps{
                input 'Please approve or deny this build'
          }
    }

  }
}