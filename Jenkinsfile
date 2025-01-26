pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/muzafferkahraman/deneme.git' // Replace with your repo URL
        BRANCH = 'master' // Replace with your branch
        DEST_PATH = '/tmp' // Replace with the target path
        FILE_TO_COPY = 'src/deneme/basic_functions.py' // File to copy from the repo
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: "${BRANCH}", url: "${REPO_URL}"
            }
        }

        stage('Run Unit Tests') {
            steps {
                script {
                    // Run tests (adjust command for your language/framework)
                    def testResult = sh(script: 'python3 -m unittest discover -s tests', returnStatus: true)
                    if (testResult != 0) {
                        error("Unit tests failed!")
                    }
                }
            }
        }

        stage('Copy File') {
            steps {
                script {
                    // Copy file to destination path
                    sh "cp ${WORKSPACE}/${FILE_TO_COPY} ${DEST_PATH}/"
                }
            }
        }
    }

    post {
        failure {
            echo "Pipeline failed. Check the logs for details."
        }
        success {
            echo "Pipeline succeeded. File copied to ${DEST_PATH}."
        }
    }
}

