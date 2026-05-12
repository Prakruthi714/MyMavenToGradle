pipeline {
    agent any

    tools {
        jdk 'JDK11'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Prakruthi714/MyMavenToGradle.git'
            }
        }

        stage('Give Permission') {
            steps {
                sh 'chmod +x gradlew'
            }
        }

        stage('Clean Project') {
            steps {
                sh './gradlew clean'
            }
        }

        stage('Build Project') {
            steps {
                sh './gradlew build'
            }
        }

        stage('Run Tests') {
            steps {
                sh './gradlew test'
            }
        }

        stage('Archive JAR') {
            steps {
                archiveArtifacts artifacts: 'build/libs/*.jar',
                                 fingerprint: true
            }
        }
    }

    post {

        always {
            junit allowEmptyResults: true,
                  testResults: 'build/test-results/test/*.xml'
        }

        success {
            echo 'Build Successful'
        }

        failure {
            echo 'Build Failed'
        }
    }
}
