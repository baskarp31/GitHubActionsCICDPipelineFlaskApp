pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
               // checkout([$class: 'GitSCM', branches: [[name: 'main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/baskarp31/GitHubActionsCICDPipelineFlaskApp.git']]])
                git branch: 'main', url: 'https://github.com/baskarp31/GitHubActionsCICDPipelineFlaskApp.git'
            }
        }
        stage('Build') {
            steps {
                git branch: 'main', url: 'https://github.com/baskarp31/GitHubActionsCICDPipelineFlaskApp.git'
                sh 'python3 app.py'
            }
        }
        stage('Test') {
            steps {
                sh 'python3 -m pytest'
            }
        }
    }
}
