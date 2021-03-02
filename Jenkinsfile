pipeline {
  agent { label 'jnode' }
  stages { 
    stage('Docker Build') {
      steps {
        sh "echo ${env.BUILD_NUMBER}"
        sh "docker build --no-cache -t anguler:01 ."
      }
    }
        
  }
  post {
    always {
      deleteDir() /* cleanup the workspace */
    }
  }
}
