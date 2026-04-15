pipeline{
    agent any

    tools {
        maven 'maven'
    }
    parameters {
        choice(name: 'BRANCH_NAME', choices: ['main', 'test'], description: 'Choose the branch to build')
        string(name: 'SLEEP_TIME', defaultValue: '10', description: 'Enter the sleep time')
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
                        for (int i = 0; i < 30; i++) {
                            echo "${i + 1}"
                            sleep 1
                        }
                        sh 'mvn test'
                        //junit(testResults: 'target/surefire-reports/TST-*.xml', keepProperties: true, keepTestNames: true)
                }
            }
        }
        stage('deploy'){
            steps {
                sh 'java -jar target/*.jar &'
            }
        }
        stage('integration-test'){
            steps {
                sh 'curl http://localhost:8080/hello'
            }
        }
        }
    }
