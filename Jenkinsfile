pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package '
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        
        stage('upload artifact to nexus'){
            steps {
               nexusArtifactUploader artifacts: 
                   [ 
                       [
                           artifactId: 'my-app', 
                           classifier: '', 
                           file: 'target/my-app-1.0-SNAPSHOT.jar',
                           type: 'jar'
                       ]
                   ],
                   credentialsId: 'b4b22ac4-cc33-444a-a50c-945f6eb4edc8',
                   groupId: 'com.mycompany.app',
                   nexusUrl: '172.31.33.156:8081',
                   nexusVersion: 'nexus3',
                   protocol: 'http', 
                   repository: 'CR1', 
                   version: '1.0-SNAPSHOT'
            }
        }
    }
}
