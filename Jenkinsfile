pipeline {

    agent any

    stages {

        stage("Git Checkout"){
            steps {
                git branch: 'main', url: 'https://github.com/Prerna31126/java-app.git'
            }
        }

        stage("Unit Testing"){
            steps {
                sh 'mvn test'
            }
        }

        stage("Integration Testing"){
            steps {
                sh 'mvn verify -DskipUnitTests'
            }
        }

        stage("Build"){
            steps {
                sh 'mvn clean install'
            }
        }

        

        stage("Upload Artifacts to Nexus"){
            steps {
                script {
                  nexusArtifactUploader artifacts: [[artifactId: 'springboot', classifier: '', file: 'target/UPES.jar', type: 'jar']], credentialsId: 'nexsus_id', groupId: 'com.example', nexusUrl: '44.193.205.13:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'java-release', version: '1.0.0'
                }
            }
        }
    }
}
