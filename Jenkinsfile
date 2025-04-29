pipeline {
    agent any

    tools {
        maven 'Maven'  // Name as configured in Global Tool Configuration
        jdk 'JDK'      // Name as configured in Global Tool Configuration
    }

    environment {
        // Set JAVA_HOME dynamically using the Jenkins tool step
        JAVA_HOME = "${tool 'JDK'}"
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Verify Java & Maven setup
                sh 'echo "JAVA_HOME is: $JAVA_HOME"'
                sh 'java -version'
                sh 'mvn -version'

                // Build with Maven
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
