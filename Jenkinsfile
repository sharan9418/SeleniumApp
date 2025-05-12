pipeline {
    agent any

    tools {
        maven 'Maven'  // Name must match Maven installation in Jenkins Global Tool Config
        jdk 'JDK'      // Name must match JDK installation in Jenkins Global Tool Config
    }

    environment {
        // Set ChromeDriver path if not set globally or using Docker image with it pre-installed
        CHROMEDRIVER_PATH = "/usr/local/bin/chromedriver"
    }

    stages {
        stage('Checkout') {
            steps {
                // Clone your GitHub repo's master branch
                git branch: 'master', url: 'https://github.com/SHASHANK9060/SeleniumApp.git'
            }
        }

        stage('Set Permissions (Optional)') {
            steps {
                // Ensure ChromeDriver is executable
                sh 'chmod +x ${CHROMEDRIVER_PATH}'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                // If you have actual test cases under src/test, they run here
                sh 'mvn test'
            }
        }

        stage('Run Selenium Application') {
            steps {
                // Runs your Selenium-based Java main class
                sh 'mvn exec:java -Dexec.mainClass="com.example.App"'
            }
        }
    }

    post {
        success {
            echo '🎉 Pipeline completed successfully!'
        }
        failure {
            echo '❌ Pipeline failed!'
        }
    }
}
