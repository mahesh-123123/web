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
    }
}
