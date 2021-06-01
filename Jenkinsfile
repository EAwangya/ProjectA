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
                script { 
                    def NexusRepo = VERSION.endsWith("SNAPSHOT") ? "ErnestDevOpsLab-SNAPSHOT" : "ErnestDevOpsLab-RELEASE"
                nexusArtifactUploader artifacts: [[artifactId: "${ARTIFACTID}",
                classifier: '',
                file: "target/${ARTIFACTID}-${VERSION}.war",
                type: 'war']],
                credentialsId: '145106b6-0808-4356-8a63-fef9975b6daf',
                groupId: 'com.ernestdevopslab', 
                nexusUrl: '18.215.251.228:8081',
                nexusVersion: 'nexus3',
                protocol: 'http', 
                repository: "${NexusRepo}",
                version: "${VERSION}"
            }
        }
   }   
        stage('Deploy') {
            steps {
                echo 'Deploying'
            }
        }
        
    }
}
