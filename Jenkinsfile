pipeline {
  agent any
  // any, none, label, node, docker, dockerfile, kubernetes
  tools {
    maven 'my_maven'
  }
  environment {
    gitName = 'oolralra'
    gitEmail = 'oolralra@gmail.com'
    githubCredential = 'git_cre'
    dockerHubRegistry = '10.7.7.0/sbimage'
    githubWeb = 'https://github.com/oolralra/sb_code'
  }

  stages {
    stage('Checkout Github') {
      steps {
          checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: githubCredential, url: githubWeb]]])
          }
      post {
        failure {
          echo 'Repository clone failure'
        }
        success {
          echo 'Repository clone success'  
        }
      }
    }

    
  }
}
