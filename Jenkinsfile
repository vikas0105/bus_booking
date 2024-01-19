pipeline {
    agent { label 'java' }
    stages {
        stage('checkout') {
            steps {
                sh 'rm -rf bus_booking'
                sh 'git clone https://github.com/yatheesh2328/bus_booking.git'
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
                        id: "artifact",
                        url: "http://13.40.110.196:8081/artifactory",
                        username: "admin",
                        password: "Aeiou@2823"
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
