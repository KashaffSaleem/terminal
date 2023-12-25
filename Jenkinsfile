pipeline {
    agent any

  stages {
        stage('Build') {
            steps {
                script {
                    // Build the Docker image
                    dockerImage = docker.build("kashafsaleem/flask-web-app")
                }
            }
        }

  stage('Test') {
            steps {
                // Run test cases (integrate with your testing framework)
                // Example: sh 'pytest tests/'
            }
        }

    stage('Deploy') {
            steps {
                script {
                    // Deploy the Docker image to your environment
                    // Example: sh 'docker run kashafsaleem/flask-web-app'
                }
            }
        }
    }

  post {
        success {
            script {
                docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                    dockerImage.push()
                }
            }
        }

        failure {
            // Rollback logic (e.g., redeploy previous version)
            mail to: 'fa20-bse-048@cuiatk.edu.pk', subject: 'Deployment Failed', body: 'Please investigate the failed deployment.'
        }
    }
}


