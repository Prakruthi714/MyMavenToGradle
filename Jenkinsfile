pipeline {
    agent any

    tools {
        jdk 'JDK17'
        gradle 'Gradle'
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
                sh 'gradle clean'
            }
        }

        stage('Build Project') {
            steps {
                sh 'gradle build'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'gradle test'
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
