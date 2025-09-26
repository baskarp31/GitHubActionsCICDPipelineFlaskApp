pipeline {
    agent any

    environment {
        // Define any environment variables you need, e.g. Python version, venv path, etc.
        PYTHON = "python3"
        VENV = "${WORKSPACE}/venv"
    }

    stages {
        stage('Checkout') {
            steps {
                //checkout scm
                git branch: 'main', url: 'https://github.com/baskarp31/GitHubActionsCICDPipelineFlaskApp.git'
            }
        }

        stage('Setup Python Environment') {
            steps {
                script {
                    // Create virtualenv
                    sh "${env.PYTHON} -m venv ${env.VENV}"
                    sh """
                        source ${env.VENV}/bin/activate
                        pip install --upgrade pip
                        pip install -r requirements.txt
                    """
                }
            }
        }

        stage('Lint / Static Analysis') {
            steps {
                script {
                    sh """
                        source ${env.VENV}/bin/activate
                        # you can add linters like flake8, pylint etc.
                        flake8 .
                    """
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    sh """
                        source ${env.VENV}/bin/activate
                        pytest --maxfail=1 --disable-warnings -q
                    """
                }
            }
            post {
                always {
                    junit '**/reports/*.xml'   // assuming you output JUnit-style XMLs
                }
            }
        }

        stage('Build / Package') {
            steps {
                script {
                    sh """
                        source ${env.VENV}/bin/activate
                        # If you want to package into a wheel or Docker image etc.
                        # Example: python setup.py bdist_wheel
                    """
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Example: deploy to a server or container
                    // You might use SSH, Docker, Kubernetes, etc.
                    sh """
                        # e.g., scp, ssh commands
                        echo "Deploying application..."
                    """
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline succeeded!"
        }
        failure {
            echo "Pipeline failed!"
        }
        always {
            // Clean up workspace or venv if needed
            cleanWs()
        }
    }
}
