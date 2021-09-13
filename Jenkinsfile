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
                deploy adapters: [tomcat9(credentialsId: 'webserver', path: '', url: 'http://localhost:8080/')], contextPath: 'war6', war: '**/*.war'
            }
        }
       /* stage('login') {
            steps {
                login  'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR'
            }
        }
        stage('push') {
            steps {
                push 'docker push maheshreddy123/war5:latest'
            }
        } */
        stage('email') {
            steps {
                mail bcc: '', body: '''hi welcome to jenkins email alerts
                thanks
                msr''', cc: '', from: '', replyTo: '', subject: 'jenkins job', to: 'mmssrraju123@gmail.com'
            }
        }
    }
         /*post {
            always {
                sh 'docker logout'
            }
        }*/
}
