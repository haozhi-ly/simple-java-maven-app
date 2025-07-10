pipeline {
    agent any
    tools { maven 'Maven3' }
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') {
            steps {
                withMaven(mavenSettingsConfig: '3ab10412-1b5c-4888-86d2-e53d3f0b3ac3') {
                    sh 'mvn -B -DskipTests clean package'
                }
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
        stage('Deliver') { 
            steps {
                sh './jenkins/scripts/deliver.sh' 
            }
        }
    }
}
