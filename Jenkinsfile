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
                    def payload = readJSON text: httpRequest(url: '', authentication: 'githubToken').getContent()
                    echo payload
                    echo ${payload}
                    // def htmlUrl = payload.pull_request.html_url
                    // echo "PR URL: ${htmlUrl}"

                }
            }
        }

    }
}
