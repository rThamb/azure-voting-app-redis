pipeline {
    agent any

    stages {
        stage('Verify Branch') {
            steps {
                echo "$GIT_BRANCH"
            }
        }
        stage('Build Docker') {
            steps {
                pwsh(script: 'docker images -a')
                pwsh(script: ""
                    "
                        cd azure - vote /
                        docker build - t jenkins - pipeline.docker images - a 
                        cd..
                    """)
            }
        }
        stage('Start App') {
            steps {
                pwsh(script: ""
                    "
                    . / scripts / test_container.psl ""
                    ")
            }
            post {
                success {
                    echo "App started successfully"
                }
                failure {
                    echo "App failed"
                }
            }
        }
        stage('Run Tests') {
            steps {
                pwsh(script: '. / test / test_sample.py')
            }
        }
        stage('Stop App') {
            steps {
                pwsh(script: 'docker-compose down')
            }
        }
    }
}
