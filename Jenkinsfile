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
                sh '/var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/Maven_path/bin/mvn clean install package'
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
                    publishers: [
                        sshPublisherDesc(
                            configName: 'DevServer',
                            transfers: [
                                sshTransfer(
                                    sourceFiles: 'webapp/target/*.war',
                                    remoteDirectory: '/root/artifacts',
                                )
                            ]
                        )
                    ]
                )
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKERHUB_USER', passwordVariable: 'DOCKERHUB_PASS')]) {
                    sh '''
                        cd /home/dockeruser/DockerFiles
                        docker build -t vuppala360/venkatdockerwithtomcat:${BUILD_NUMBER} .
                        docker login -u $DOCKERHUB_USER --password $DOCKERHUB_PASS
                        docker push vuppala360/venkatdockerwithtomcat:${BUILD_NUMBER}
                    '''
                }
            }
        }
    }
}

