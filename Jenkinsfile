pipeline {
    agent any
        tools {
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
                echo 'Testing ......'
            }
        }
        stage('Publish to Nexus') {
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'ErnestDevOpsLab',
                classifier: '',
                file: 'target/ErnestDevOpsLab-0.0.3-SNAPSHOT.war',
                type: 'war']],
                credentialsId: '132a42f4-5f0d-4a6a-84fb-6988a15236bb',
                groupId: 'com.ernestdevopslab', 
                nexusUrl: '54.196.105.192:8081',
                nexusVersion: 'nexus3',
                protocol: 'http', 
                repository: 'ErnestDevopsLab-SNAPSHOT',
                version: '0.0.3-SNAPSHOT'
            }
        }
       stage('Print Environmental Variables') {
            steps {
                echo "Artifact ID is '${ArtifactId}'"
                echo "Version is '${Version}'"
                echo "GroupID is '${GroupId}'"
                echo "Name is '${Name}'"
            }
        } 
        stage('Deploy') {
            steps {
                echo 'Deploying'
            }
        }
        
    }
}
