pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Checkout source code from the repository
                git 'https://github.com/venkatavuppala/cicd-test.git'

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
