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
                    // sh "export OPENAI_API_KEY=${OPENAI_API_KEY}"
                    
                    echo "PR URL: ${PR_URL}"

                    echo "Started REVIEW"

                    withCredentials([string(credentialsId: 'GH_TOKEN', variable: 'GH_TOKEN')]) {

                    REVIEW = sh(script: "gptscript codereview.gpt --PR_URL=${PR_URL}", returnStdout: true).trim()

                    replacedText = REVIEW.replaceAll(~/\n/, "<br>")

                    sh "curl -H \"Authorization: Token ${GH_TOKEN}\" -X POST -d '{\"body\": \"${replacedText}\"}' '${PR_COMMENTS_URL}'"

                    if (REVIEW.contains('Require Changes')) {
                        echo 'Code Requires Changes'
                        currentBuild.result = 'FAILURE' // Mark the build as failed
                        error 'Code Requires Changes' // Terminate the build with an error
                    }
                    
                    // Check if REVIEW contains 'Approved'
                    if (REVIEW.contains('Approved')) {
                        echo 'Code Approved'
                        // Additional steps if needed for approval
                    }


                    }

                    }
                }
            }
        }

    }

}
