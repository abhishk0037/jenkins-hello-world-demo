pipeline{
    agent any

    tools {
        maven 'maven'
    }

    stages {
        stage('Echo Version') {
            steps {
                sh 'echo Print Maven Version'
                sh 'mvn -version'
            }
        }

        stage('build') {
            steps {
                git branch: 'main', url: 'https://github.com/abhishk0037/jenkins-hello-world-demo.git'
                sh 'mvn clean package -DskipTests=true'
                }
            }
        stage('unit test'){
            steps {
                sh 'mvn test'
            }
        }
    }
}