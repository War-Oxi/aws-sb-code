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
        DOCKERCREDENTIAL = 'docker_credential'
        DOCKERHUB = 'kkankkandev/spring'


    }
    
    stages {
        stage('Checkout Github') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [],
                userRemoteConfigs: [[credentialsId: GITCREDENTIAL, url: GITWEBADD]]])
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
        
        stage('code build') {
            steps {
                sh "mvn clean package"
            }
        }
        stage('image build') {
            steps {
                sh "docker build -t ${DOCKERHUB}:${currentBuild.number} ."
                // currentBuild.numer = 젠킨스가 제공하는 빌드넘버 변수
                // kkankkandev/spring:1 같은 형태로 빌드가 될 예정정
            }
        }
        stage('image push') {
            steps {
                sh "docker push ${DOCKERHUB}:${currentBuild.number}"
                sh "docker push ${DOCKERHUB}:latest"
            }
            
            post {
                failure {
                    echo 'docker image push fail'
                    sh "docker image rm -f ${DOCKERHUB}:${currentBuild.number}"
                    sh "docker image rm -f ${DOCKERHUB}:latest"
                }
                success {
                    echo 'docker image push success'
                    sh "docker image rm -f ${DOCKERHUB}:${currentBuild.number}"
                    sh "docker image rm -f ${DOCKERHUB}:latest"
                }
            }
        }
    }
}