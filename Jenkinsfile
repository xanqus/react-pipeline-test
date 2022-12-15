pipeline {
    agent any

    tools {
        docker 'latest'
        // jdk 'your_jdk_version'
    }

    stages {
        stage('connect test'){
            steps{
                sh """
                echo connect
                """
            }
        }
         stage('Build') {
            agent {
                docker {
                    image 'node:18.12.1-alpine'
                }
            }
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
    }
}