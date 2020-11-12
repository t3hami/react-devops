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
                sh 'docker build -t tehami/react:1.0 .'
            }
        }
        stage('Docker Push') {
            steps {
                withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId:'dockerhub-creds',
                                  usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD'] ]){
                    sh 'docker login -u $USERNAME -p $PASSWORD'
                    sh 'docker push tehami/react:1.0'
                    sh 'docker logout'
                }
            }
        }
    }
}
