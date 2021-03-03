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
        withCredentials([usernamePassword(credentialsId: 'a7d170b9-3213-4dc4-a055-8d095d967f64', passwordVariable: 'Password', usernameVariable: 'Username')]) {
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
