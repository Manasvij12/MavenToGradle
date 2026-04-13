pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'JDK'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Manasvij12/MavenToGradle.git'
            }
        }

        // -------------------------
        // MAVEN BUILD (OLD SYSTEM)
        // -------------------------
        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test with Maven') {
            steps {
                sh 'mvn test'
            }
        }

        // -------------------------
        // GRADLE BUILD (NEW SYSTEM)
        // -------------------------
        stage('Build with Gradle') {
            steps {
                sh './gradlew clean build'
            }
        }

        stage('Test with Gradle') {
            steps {
                sh './gradlew test'
            }
        }

        // -------------------------
        // RUN APPLICATION
        // -------------------------
        stage('Run Application') {
            steps {
                sh './gradlew run'
            }
        }

        // -------------------------
        // VERIFY OUTPUT
        // -------------------------
        stage('Compare Artifacts') {
            steps {
                sh 'ls -l target/'
                sh 'ls -l build/libs/'
            }
        }
    }

    post {
        success {
            echo '✅ Maven to Gradle pipeline successful!'
        }
        failure {
            echo '❌ Pipeline failed!'
        }
    }
}
