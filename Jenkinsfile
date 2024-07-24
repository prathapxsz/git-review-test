pipeline {
    agent any

    environment {
        GITHUB_TOKEN = credentials('github-gpt') // GitHub personal access token credential ID
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Checkout the pull request branch
                    checkout([$class: 'GitSCM',
                              branches: [[name: "*/${env.CHANGE_BRANCH}"]],
                              extensions: [[$class: 'CleanCheckout']],
                              userRemoteConfigs: [[
                                  url: 'https://github.com/prathapxsz/git-review-test.git',
                                  credentialsId: 'github-gpt'
                              ]]]
                    )
                }
            }
        }

        stage('Review Pull Request') {
            steps {
                script {
                    // Change directory to where the test file is located
                    dir('test-file.txt') {
                        // Check if 'fail' keyword exists in the test file
                        def keywordFound = sh(script: "grep -q 'fail' test_file.txt", returnStatus: true)
                        if (keywordFound == 0) {
                            currentBuild.result = 'FAILURE'
                            error "PR contains 'fail'. Marking the PR as failed."
                        } else {
                            currentBuild.result = 'SUCCESS'
                            echo "No 'fail' found. PR passes."
                        }
                    }
                }
            }
        }
    }
}
