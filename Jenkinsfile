pipeline {
  agent any 
  triggers {
    githubPush()
  }
  stages {
    stage ('Pre-build: Syntax Checks') {
           steps {
             script {
               sh 'echo "Performing syntax checks..."'
             }
           }
    }
    stage ('Build') {
      steps{
        script {
          sh './gradlew build'
        }
      }
    }
    stage ('Unit Test and Code Coverage') {
      steps {
        script {
          sh './gradlew test'
        }
        junit '**/build/test-results/test/*.xml'
      }
    }
  }

post {
  always {
    mail to : 'Veeramally.Supriya@ltts.com',
      subject : "Build Status: ${currentBuild.currentResult}",
      body : "Build ${env.BUILD_URL} finished with status: ${currentBuild.currentResult}\n\nLogs:\n${env.BUILD_URL}console"
  }
}
}
           
