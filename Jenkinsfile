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
            docker build - t jenkins - pipeline.docker images - a cd..
            ""
            ")
          }
        }

        stage('Start app') {
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

          stage('Run tests') {
            steps {
              pwsh(script: ""
                "
                . / test / test_sample.py ""
                ")
              }
            }

            stage('Stop test app') {
              steps {
                pwsh(script: 'docker-compose down')
              }
            }

    }
}