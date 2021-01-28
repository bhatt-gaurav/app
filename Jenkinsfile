pipeline {
    agent any 
    tools{
      maven 'maven'
   }
    environment {
      ArtifactId = readMavenPom().getArtifactId()
      Version = readMavenPom().getVersion()
      Name = readMavenPom().getName()
      GroupId = readMavenPom().getGroupId()
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
             nexusArtifactUploader artifacts: [[artifactId: "${ArtifactId}", classifier: '', file: 'target/WebApp-2.0.2-SNAPSHOT.war', type: 'war']], credentialsId: 'bb1e4e43-9809-41eb-a535-fc1217f9089a', groupId: "${GroupId}", nexusUrl: '172.20.10.8:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshot', version: "${Version}"
            }
        }
        // Stage 4 : Print some information
        stage ('Print Environment variables'){
                    steps {
                        echo "Artifact ID is '${ArtifactId}'"
                        echo "Version is '${Version}'"
                        echo "GroupID is '${GroupId}'"
                        echo "Name is '${Name}'"
                    }
         }
        stage('Deploy') { 
            steps {
                echo 'deploying....'
            }
        }
    }
}
