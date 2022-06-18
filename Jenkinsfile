pipeline {
  agent any
   environment {
   ANSIBLE_PRIVATE_KEY=credentials('ansible-key') 
  }

  stages {

    stage('Git checkout branch') {
      steps {
        checkout([
          $class: 'GitSCM', branches: [
            [name: '*/main']
          ],
          userRemoteConfigs: [
            [url: 'http://10.0.0.152:9999/gitlab-instance-019d8890/jenkins-ansible-k8s.git', credentialsId: 'git-checkout-user']
          ]
        ])
        sh "pwd"
        sh "ls -ltr"
      }

      
    }

     stage('Run ansible playbook') {
      steps {
       
       sh "ansible-playbook -i /var/lib/jenkins/workspace/ansible-k8s-pipeline/inventory/k8s.hosts --private-key=$ANSIBLE_PRIVATE_KEY  /var/lib/jenkins/workspace/ansible-k8s-pipeline/playbook.yml"
      }

      
    }
  }
}