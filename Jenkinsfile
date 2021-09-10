pipeline {
    agent any

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
                deploy adapters: [tomcat9(credentialsId: 'webserver', path: '', url: 'http://localhost:8080/')], contextPath: 'war2', war: '**/*.war'
            }
        }
        stage('push') {
            steps {
                 docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {

        def customImage = docker.build("maheshreddy123/dockerwebapp")

        /* Push the container to the custom Registry */
        customImage.push()
               }
                
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
