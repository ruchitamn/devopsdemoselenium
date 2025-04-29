pipeline {
    agent any

    tools {
        maven 'Maven'  // Replace with actual tool name from Jenkins configuration
        jdk 'JDK'      // Replace with actual JDK tool name from Jenkins configuration
    }

    environment {
        // Dynamically set JAVA_HOME based on the Jenkins tool configuration
        JAVA_HOME = tool name: 'JDK', type: 'JDK'
        PATH = "${JAVA_HOME}/bin:${env.PATH}"  // Add JAVA_HOME to PATH
        CHROME_DRIVER_PATH = '/path/to/chromedriver'  // Replace with path to your ChromeDriver (if using Chrome)
        GECKO_DRIVER_PATH = '/path/to/geckodriver'    // Replace with path to your GeckoDriver (if using Firefox)
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm  // Checkout code from the SCM repository
            }
        }

        stage('Install Dependencies') {
            steps {
                // Ensure the required dependencies are available (like ChromeDriver, GeckoDriver, etc.)
                sh 'echo "Ensure dependencies are in place for Selenium tests."'
            }
        }

        stage('Build') {
            steps {
                // Debug step: Print JAVA_HOME and Maven version to ensure correct setup
                sh 'echo "JAVA_HOME: $JAVA_HOME"'
                sh 'echo "Maven version:" && mvn -version'  // Print Maven version
                sh 'mvn clean package'  // Run the Maven build command
            }
        }

        stage('Test') {
            steps {
                // Run Selenium tests using Maven
                sh 'mvn test -Dselenium.driver=chrome'  // Run tests (adjust for desired browser)
            }
        }

        stage('Archive Artifacts') {
            steps {
                // Archive the built artifacts (e.g., .jar files, test results)
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
                // You can also archive test reports here if needed
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'  // Success message
        }
        failure {
            echo 'Pipeline failed!'  // Failure message
        }
    }
}
