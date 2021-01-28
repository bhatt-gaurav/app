pipeline {
    agent any 
    tools{
      maven 'maven'
   }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn clean install package' 
            }
        }
        stage('Test') { 
            steps {
                echo ' testing.....' 
            }
        }
        stage('Publish to nexus') {
            steps{
             nexusArtifactUploader artifacts: [[artifactId: 'WebApp', classifier: '', file: 'target/WebApp-2.0.2-SNAPSHOT.war', type: 'war']], credentialsId: 'bb1e4e43-9809-41eb-a535-fc1217f9089a', groupId: 'lu.amazon.aws.demo', nexusUrl: '172.20.10.8:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshot', version: '2.0.2-SNAPSHOT'
            }
        }
        stage('Deploy') { 
            steps {
                echo 'deploying....'
            }
        }
    }
}
