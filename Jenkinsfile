pipeline {
    agent any

    // agent {
    //     docker {
    //         image 'node:16.13.1-alpine'
    //     }
    // }

    // agent {
    //     label 'main-host'
    // }

    // tools {
    //     docker "latest"
    // }
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

        stage('Docker build') {
            agent any
            steps {
                sh 'docker build -t my-react-app:latest .'
            }
        }

        stage('Docker run') {
            agent any
            steps {
                sh 'docker ps -f name=my-react-app -q | xargs --no-run-if-empty docker container stop'
                sh 'docker container ls -a -f name=my-react-app -q | xargs -r docker container rm'
                sh 'docker images --no-trunc --all --quiet --filter="dangling=true" | xargs --no-run-if-empty docker rmi'
                sh 'docker run -d --name {container_name} -p 8090:80 {image_name}:latest'
            }
        }
    }
}