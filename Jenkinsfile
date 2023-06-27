pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Build the Maven project
                sh "echo ' Build test'"
            }
        }

        stage('Test') {
            steps {
                // Run tests using Maven
                sh "echo 'mvn test'"
            }
        }
    }
}
