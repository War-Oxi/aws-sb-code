pipeline {
    agent any
    
    tools {
        maven 'my_maven'
    }
    environment {
        GITNAME = 'war-oxi'                 // 본인 깃허브계정
        GITMAIL = 'xowl5460@naver.com'      // 본인 이메일
        GITWEBADD = 'https://github.com/War-Oxi/aws-sb-code.git'
        GITSSHADD = 'git@github.com:War-Oxi/aws-sb-code.git'
        GITCREDENTIAL = 'github_credential'           // 아까 젠킨스 credential에서 생성한
    }
    
    stages {
        stage('Checkout Github') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [],
                userRemoteConfigs: [[credentialsId: GITCREDENTIAL, url: GITWEBADD]]])
            }
        }
        
        post {
            failure {
                echo 'Repository clone failure'
            }
            success {
                echo 'Repository clone success'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}