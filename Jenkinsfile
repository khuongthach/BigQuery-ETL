 Wpipeline {
  agent any
  stages {
    stage('Long Short') {
      parallel {
        stage('Trips') {
          steps {
            sh 'docker exec -t bigquery_etl python3 /src/src/bigquery_merge.py merge_trips	'
          }
        }

        stage('Payment') {
          steps {
            sh 'docker exec -t bigquery_etl python3 /src/src/bigquery_merge.py merge_payment'
          }
        }

      }
    }

  }
  post {
    always {
      echo 'This will always run'
    }

    success {
      echo 'This will run only if successful'
    }

    failure {
      mail(bcc: '', body: "<b>Example</b><br>\n<br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL of build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: '', mimeType: 'text/html', replyTo: '', subject: "ERROR CI: Project name -> ${env.JOB_NAME}", to: 'khuongthach93@gmail.com')
    }

  }
  triggers {
    cron('H * * * *')
  }
}
