def VERSION = "UNINTIALIZED"
def ARTIFACTID = "UNINTIALIZED"
pipeline {
    agent any


        tools {
        maven 'maven'
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install package'

             script {
                    VERSION = readMavenPom().getVersion()
                    ARTIFACTID = readMavenPom().getArtifactId()
                    
                }
                echo("VERSION=${VERSION}")
                echo("ARTIFACTID=${ARTIFACTID}")
                
                
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
                file: 'target/ErnestDevOpsLab-0.0.4-SNAPSHOT.war',
                type: 'war']],
                credentialsId: '132a42f4-5f0d-4a6a-84fb-6988a15236bb',
                groupId: 'com.ernestdevopslab', 
                nexusUrl: '54.196.105.192:8081',
                nexusVersion: 'nexus3',
                protocol: 'http', 
                repository: 'ErnestDevopsLab-SNAPSHOT',
                version: '${TAG_SELECTOR}'
            }
        }
       
        stage('Deploy') {
            steps {
                echo 'Deploying'
            }
        }
        
    }
}
