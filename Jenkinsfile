pipeline {
    agent any

    // environment {
    //     GITHUB_TOKEN = credentials('github-gpt') // GitHub personal access token credential ID
    // }

    stages {

        stage('Clean Workspace') {
            steps {
                deleteDir()
            }
        }
        
        stage('Checkout') {
            steps {
                script {

                    echo "Hello World"
                }
            }
        }

    }
}
