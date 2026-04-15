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
        stage('archive artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
        stage('unit test'){
            steps {
                 //introduce a delay of 60 seconds before executing the tests through for loop
                script {
                        for (int i = 0; i < 60; i++) {
                            echo "${i + 1}"
                            sleep 1
                        }
                sh 'mvn test'
            }
        }
    }
}