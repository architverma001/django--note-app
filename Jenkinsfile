
pipeline {
    agent { label "agent" }

    environment {
        EMAIL_RECIPIENTS = "arpitverma2410@gmail.com"
    }

    stages {


    stage('init') {
            steps {
                script {
                    echo "Initializing pipeline for branch: ${env.GIT_BRANCH}"
                    
                    // ✅ Dynamically load the shared library based on the branch
                    library("Shared@main")

                }
            }
        }

        stage("hello") {
            steps {
                script {
                    hello()
                }        
            }
        }

        stage('Cloning the Code') {
            steps {
                script {
                    clone("https://github.com/architverma001/django--note-app", "main")
                }
            }
        }

        stage('Build') {
            steps {
                echo "Building project"
                sh "docker build -t notes-app:latest ."
            }
        }

        stage('Testing the Code') {
            steps {
                echo "Testing the code"
                // Add actual test scripts if available
            }
        }

        stage('Deploying the Code') {
            steps {
                echo "Deploying the code"
                sh "docker compose down"
                sh "docker compose up -d"
            }
        }
    }

    post {
        failure {
            mail(
                to: 'arpitverma2410@gmail.com',
                cc: 'hawk90217@gmail.com',
                subject: "FAILED: Build ${env.JOB_NAME}",
                body: """Build failed: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}

View the log at:
${env.BUILD_URL}

Blue Ocean:
${env.RUN_DISPLAY_URL}"""
            )
        }

        success {
            mail(
                to: 'arpitverma2410@gmail.com',
                cc: 'hawk90217@gmail.com',
                subject: "SUCCESSFUL: Build ${env.JOB_NAME}",
                body: """Build Successful: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}

View the log at:
${env.BUILD_URL}

Blue Ocean:
${env.RUN_DISPLAY_URL}"""
            )
        }

        aborted {
            mail(
                to: 'arpitverma2410@gmail.com',
                cc: 'hawk90217@gmail.com',
                subject: "ABORTED: Build ${env.JOB_NAME}",
                body: """Build was aborted: ${env.JOB_NAME} - Build #${env.BUILD_NUMBER}

View the log at:
${env.BUILD_URL}

Blue Ocean:
${env.RUN_DISPLAY_URL}"""
            )
        }
    }
}
