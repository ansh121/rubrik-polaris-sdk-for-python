pipeline {
    agent any
    stages {
        stage('Generate Docs') {
            steps {
                sh 'chmod -R 755 .'
            /**
                sh 'sudo pip3.8 install jinja2 requests'
                sh '/usr/local/bin/python3.8 ./create_docs.py'

            **/
            }
        }
        stage('Commit Docs') {
            steps {
                echo 'Commit Docs'
                sh 'git branch'
                /**
                withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'github-user', usernameVariable: 'GIT_AUTHOR_NAME', passwordVariable: 'GIT_PASSWORD']]) {
                    sh "git commit -a -m 'Documentation Update for Commit $GIT_COMMIT'"
                    sh('git push origin $BRANCH_NAME https://${GIT_AUTHOR_NAME}:${GIT_PASSWORD}@github.com/trinity-team/rubrik-sdk-for-python.git --tags -f --no-verify')
                }
                **/
            }
        }
        stage('Function Tests') {
            agent {
                docker {
                    image 'python:3.8'
                }
            }
            steps {
                echo 'Run Tests'
                sh 'printenv'
                sh 'pwd'
                sh 'ls'
            }
        }
    }
    post {
        always {
            cleanWs()
        }
        success {
            echo 'successful'
        }
        failure {
            echo 'failed'
        }
        unstable {
            echo 'unstable'
        }
        changed {
            echo 'changed'
        }
    }
}

