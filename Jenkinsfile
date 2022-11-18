pipeline {
    agent any
    tools {
    maven 'Maven-3.8.6'
    }
      stages {
        stage('Build') {
            steps {
                echo 'TODO: build install'
                sh 'mvn clean install'
            }
        }
        stage('Package') {
            steps {
                echo 'TODO: package'
                sh 'mvn clean package -e'           
            }
        }
       // stage('Sonar') {
       //     steps {
      //           script {      
       //         withSonarQubeEnv('Sonar') {
       //         sh 'mvn clean package sonar:sonar -Dsonar.projectKey=ejemplo-nexus -Dsonar.java.binaries=build'
       //            }
       //         }
       //     }
      //  }
	stage("Publish to Nexus Repository Manager") {
            steps {
                script {
                   nexusPublisher nexusInstanceId: 'NexusServer', nexusRepositoryId: 'devops-usach-nexus', 
			packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: "${WORKSPACE}/build/DevOpsUsach2020-0.0.1.jar"]],
		        mavenCoordinate: [artifactId: 'DevOpsUsach2020', groupId: 'com.devopsusach2020', packaging: 'jar', version: '1.0.0']]]
                }
            }
        }  
	stage('Pull the file off Nexus'){
           steps{
            withCredentials([usernameColonPassword(credentialsId: 'NexusKey', variable: 'NEXUS_CREDENTIALS')]){
                sh script: 'curl -u ${NEXUS_CREDENTIALS} -o DevOpsUsach2020-0.0.1.jar "http://nexus:8081/repository/devops-usach-nexus/com/devopsusach2020/DevOpsUsach2020/0.0.1/DevOpsUsach2020-0.0.1.jar"'
            }
          }
               
        }      
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }
    }
}
