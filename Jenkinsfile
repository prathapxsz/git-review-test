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

                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: '*/gpt-dev']], // Specify branch if needed
                        userRemoteConfigs: [[
                            url: 'https://github.com/prathapxsz/git-review-test.git',
                            credentialsId: 'gpt-review-2' // Optional: If using credentials
                        ]]
                    ])


                    withCredentials([string(credentialsId: 'OPENAI_API_KEY', variable: 'OPENAI_API_KEY')]){
                    sh "gptscript --version"
                    sh "export OPENAI_API_KEY=${OPENAI_API_KEY}"
                    echo "PR URL: ${PR_URL}"
                    sh "gptscript codereview.gpt --PR_URL=${PR_URL}"
                    // sh "REVIEW=$(gptscript codereview.gpt --PR_URL=${PR_URL})" 


                    }
                }
            }
        }

    }
}
