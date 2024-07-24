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

        stage('GPT Review') {
            steps {
                script {
                    echo "Hello World"
                    def payload = readJSON text: env.CHANGE_PAYLOAD // Assuming CHANGE_PAYLOAD contains the JSON payload
                    
                    // Example: Accessing pull request number
                    def prNumber = payload.pull_request.number
                    echo "Pull Request Number: ${prNumber}"

                    // def htmlUrl = payload.pull_request.html_url
                    // echo "PR URL: ${htmlUrl}"

                }
            }
        }

    }
}
