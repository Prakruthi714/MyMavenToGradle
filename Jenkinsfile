pipeline {
    agent any

    tools {
        jdk 'JDK'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'master',
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

        success {
            echo 'Build Successful'
        }

        failure {
            echo 'Build Failed'
        }

        always {
            junit 'build/test-results/test/*.xml'
        }
    }
}
