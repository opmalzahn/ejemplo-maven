pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'TODO: build'
                sh './mvnw clean compile -e'
            }
        }
        stage('Sonar') {
            steps {
                script {      
                    withSonarQubeEnv('SonarTest') {
                        sh './mvnw clean package sonar:sonar'
                    }
                }
            }
        }
        stage('Test') {
            steps {
                echo 'TODO: test'
                sh './mvnw clean test -e'
            }
        }
        stage('Package') {
            steps {
                echo 'TODO: package'
                sh './mvnw clean package -e'           
            }
        }
        stage('Run') {
            steps {
                echo 'TODO: run'
                sh 'nohup bash ./mvnw spring-boot:run &'         
                cleanWs()
            }
        }
    }
}
