pipeline {
    agent any

    tools {
        maven 'Maven' // Make sure Maven is configured in Jenkins Global Tools Configuration
    }
    
    stages {
        stage('Checkout Code') {
            steps {
                echo 'Checking out code...'
                git branch: 'master', url: 'https://github.com/akshayrapatwar/mavendemo.git'
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
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }
    }
}

