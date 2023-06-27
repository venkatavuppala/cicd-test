pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Build the Maven project
                sh "echo 'Build test'"
            }
        }

        stage('Test') {
            steps {
                // Run tests using Maven
                sh "echo 'mvn test'"
            }
        }

        stage('Poststage') {
            steps {
                // Running shell commands
                sh 'echo "Executing poststage command"'
                sh 'ls -al'
                sh 'pwd'
            }
        }

        stage('SSH') {
            steps {
                // SSH task
                sh 'sshpass -p "junk1@junk" ssh root@51.141.100.230 ls -l /tmp'
            }
        }
    }
}
}

