pipeline {
    agent { label 'agent-node1' }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t tehami/react .'
            }
        }
        stage('Docker Push') {
            steps {
                sh 'echo Pushing image to docker hub...'
                withDockerRegistry([ credentialsId: "dockerhub-creds" ]) {
                    sh 'docker push tehami/react'
                }
            }
        }
    }
}
