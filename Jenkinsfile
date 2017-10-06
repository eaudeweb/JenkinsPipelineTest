pipeline {
  agent any
  stages {
    stage('Message') {
      steps {
        parallel(
          "Print Message": {
            echo 'Test Message'
            
          },
          "Print Message 2": {
            echo 'Second test message'
            
          }
        )
      }
    }
  }
  environment {
    GIT_NAME = 'JenkinsPipelineTest'
  }
  post {
    changed {
      script {
        def url = "${env.BUILD_URL}/display/redirect"
        def status = currentBuild.currentResult
        def subject = "${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
        def summary = "${subject} (${url})"
        def details = """<h1>${env.JOB_NAME} - Build #${env.BUILD_NUMBER} - ${status}</h1>
        <p>Check console output at <a href="${url}">${env.JOB_BASE_NAME} - #${env.BUILD_NUMBER}</a></p>
        """
        
        def color = '#FFFF00'
        if (status == 'SUCCESS') {
          color = '#00FF00'
        } else if (status == 'FAILURE') {
          color = '#FF0000'
        }
        slackSend (color: color, message: summary)
        emailext (subject: '$DEFAULT_SUBJECT', to: '$DEFAULT_RECIPIENTS', body: details)
      }
      
      
    }
    
  }
}
