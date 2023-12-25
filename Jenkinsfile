pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    // Your build steps here
                    echo 'Building the Docker image...'
                    dockerImage = docker.build("your-docker-hub-username/your-image-name")
                }
            }
        }

        stage('Test') {
            steps {
                // Run test cases (integrate with your testing framework)
                // Example: sh 'pytest tests/'
                echo 'Running tests...'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Your deployment steps here
                    echo 'Deploying the Docker image...'
                }
            }
        }
    }

    post {
        success {
            script {
                // Push the Docker image on success
                docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                    dockerImage.push()
                }
            }
        }

        failure {
            // Rollback logic (e.g., redeploy previous version)
            echo 'Deployment Failed. Rolling back...'
            mail to: 'fa20-bse-048@cuiatk.edu.pk', subject: 'Deployment Failed', body: 'Please investigate the failed deployment.'
        }
    }
}
s
