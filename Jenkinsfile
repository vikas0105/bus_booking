@Library('jenkins-shared-libraries-@main') _  // Correct syntax

pipeline {
    agent { label 'slave' }

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'
        MAVEN_HOME = '/usr/share/maven'
        PATH = "${JAVA_HOME}/bin:${MAVEN_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout Code') {
            steps {
		script {
			pipeline1.checkscm()
		}		
       	}
     }
        stage('Set up Java 17') {
            steps {
                script {
                	pipeline1.setupjava()
                }
            }
	}

        stage('Set up Maven') {
            steps {
                script {
                	pipeline1.mavensetup()
		}
            }
        }

        stage('Build with Maven') {
            steps {
                script {
			pipeline1.build()
		}
            }
        }

        stage('Upload Artifact') {
            steps {
                uploadArtifact('target/bus-booking-app-1.0-SNAPSHOT.jar')
            }
        }

        stage('Run Application') {
            steps {
                script {
				pipeline1.runApp()
				}
            }
        }

        stage('Validate App is Running') {
          	steps {
               	script {
					pipeline1.validateApp()
				}
			}
        }
        stage('wait') {
			steps {
				script {
					pipeline1.waiting()
				}
			}
        }
        stage('stoping') {
			steps {
				script {
					pipeline1.stop()
				}
			}
        }
         stage('cleaning') {
			steps {
				script {
					pipeline1.clean()
				}
			}
        }        
    }
}
