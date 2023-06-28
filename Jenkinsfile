pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Checking out code...'
                git 'https://github.com/akshayrapatwar/mavendemo.git'
            }
        }

        stage('Build with Maven') {
            steps {
                echo 'Building with Maven...'
                sh 'mvn clean install package'
            }
        }

        stage('Archive WAR') {
            steps {
                echo 'Archiving WAR file...'
                archiveArtifacts artifacts: 'webapp/target/*.war', fingerprint: true
            }
        }

        stage('Deploy to DevServer') {
            steps {
                echo 'Deploying to DevServer...'
                sshPublisher(
                    continueOnError: false,
                    failOnError: true,
                    publishers: [
                        sshPublisherDesc(
                            configName: "DevServer",
                            transfers: [
                                sshTransfer(
                                    sourceFiles: "webapp/target/*.war",
                                    remoteDirectory: "/root/artifacts"
                                )
                            ]
                        )
                    ]
                )
            }
        }
    }
}

