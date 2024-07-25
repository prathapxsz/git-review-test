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

                    withCredentials([string(credentialsId: 'OPENAI_API_KEY', variable: 'OPENAI_API_KEY')]){
                    // echo ${OPENAI_API_KEY}
                    echo "Echoing the key"
                    echo OPENAI_API_KEY
                    echo "Exporting the open key here"
                    sh "export OPENAI_API_KEY=${OPENAI_API_KEY}"
                    echo "PR URL: ${PR_URL}"
                    sh "curl https://get.gptscript.ai/install.sh"
                    sh "sh install.sh"
                    sh "gptscript codereview.gpt --PR_URL=${PR_URL}"
                    // sh "REVIEW=$(gptscript codereview.gpt --PR_URL=${PR_URL})" 

                    }
                }
            }
        }

    }
}
