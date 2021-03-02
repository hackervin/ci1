pipeline {
  agent { label 'jnode' }
  stages { 
    stage('Docker Build') {
      steps {
        sh "echo ${env.BUILD_NUMBER}"
        sh "docker build --no-cache -t anguler:01 ."
      }
    }
    
    stage('Docker Push') {
      steps {
        withCredentials([usernamePassword(credentialsId: '6712fc73-0879-440d-a3ab-4a60e7f3336f', passwordVariable: 'Password', usernameVariable: 'Username')]) {
          sh "docker login -u ${env.Username} -p ${env.Password}"
          sh "docker push hackervin/anguler:01"
        }
      }
    }
    stage('Launch Container') {
      steps {
        sh "docker run -d --restart=always --name anguler -p 80:80 hackervin/anguler:01"
      }
    }    
  }
  post {
    always {
      deleteDir() /* cleanup the workspace */
    }
  }
}
