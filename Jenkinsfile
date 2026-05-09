pipeline {
    agent any

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk'
        MAVEN_HOME = '/usr/share/maven'
        PATH = "${MAVEN_HOME}/bin:${JAVA_HOME}/bin:${PATH}"
    }

    stages {
        stage('Initialize') {
            steps {
                echo "========== Pipeline Started =========="
                echo "Job: ${env.JOB_NAME}"
                echo "Build: #${env.BUILD_NUMBER}"
                echo "Workspace: ${env.WORKSPACE}"
            }
        }

        stage('Build') {
            steps {
                echo "========== Building =========="
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                echo "========== Running Tests =========="
                sh 'mvn test'
            }
        }

        stage('Archive Artifacts') {
            steps {
                echo "========== Archiving =========="
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo "✅ Build SUCCESS - #${env.BUILD_NUMBER}"
        }
        failure {
            echo "❌ Build FAILED - #${env.BUILD_NUMBER}"
        }
        always {
            echo "========== Pipeline Finished =========="
            cleanWs()
        }
    }
}
