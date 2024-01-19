pipeline {
    agent { label 'java' }
    stages {
        stage('checkout') {
            steps {
                sh 'rm -rf bus_booking'
                sh 'git clone https://github.com/tarundanda147/bus_booking.git'
            }
        }

        stage('build') {
            steps {
                script {
                    sh "mvn clean install"
                }
            }
        }
		stage('Deploy to JFrog Artifactory') {
            steps {
               // Remember this is the step which I followed for free style project.
                script {
                    rtServer(
                        id: "Artifact",
                        url: "http://13.238.154.172:8081/artifactory",
                        username: "jenkins",
                        password: "passwd"
                    )
                }
            }
        }

        stage('Upload') {
            steps {
                script {
		// For my  undertanding rtUpload is a part of jFrog Artifactory plugin to upload artifacts to artifacts repo
                    rtUpload (
                        serverId: 'Artifact',
                        spec: '''{
                            "files": [
                                {
                                    "pattern": "target/*.jar",
                                    "target": "libs-release-local/"
                                }
                            ]
                        }'''
                    )
                }
            }
        }

        stage('Publish build info') {
            steps {
                script {
		    // For my understanding to publish build info
                    rtPublishBuildInfo serverId: "Artifact"
                }
            }
        }
    }
}
