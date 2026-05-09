pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Hello from Jenkins'
                echo "Job: ${env.JOB_NAME}"
                echo "Build: #${env.BUILD_NUMBER}"
            }
        }
    }
    post {
        always {
            echo 'Done'
        }
    }
}
