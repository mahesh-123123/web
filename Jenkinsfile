pipeline {
    agent any
    environment{
        DOCKERHUB_CREDENTIALS=credentials('dockerhub')
    }

    stages {
        stage('war2') {
            steps {
                git branch: 'war1', url: 'https://github.com/mahesh-123123/web.git'
            }
        }
        stage('build') {
            steps {
                bat 'mvn clean'
                bat 'mvn install'
            }
        }
        stage('deploy') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'webserver', path: '', url: 'http://localhost:8080/')], contextPath: 'war4', war: '**/*.war'
            }
        }
        stage('login') {
            steps {
                sh ' echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR
            }
        }
        stage('push') {
            steps {
                sh 'docker push maheshreddy123/war4:latest'
            }
        }
        post {
            always {
                sh 'docker logout'
            }
        }
        
        stage('email') {
            steps {
                mail bcc: '', body: '''hi welcome to jenkins email alerts
                thanks
                msr''', cc: '', from: '', replyTo: '', subject: 'jenkins job', to: 'mmssrraju123@gmail.com'
            }
        }
    }
}
