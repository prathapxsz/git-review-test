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
                    sh "curl https://get.gptscript.ai/install.sh | sh"
                    def htmlUrl = payload.pull_request.html_url
                    echo "PR URL: ${htmlUrl}"

                }
            }
        }

    }
}
