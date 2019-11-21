pipeline {
  environment {
    registry = "gustavoapolinario/docker-test"
    registryCredential = 'docker-credentials'
    dockerImage = ''
  }
  agent any

  stages {
    stage('Cloning Git') {
      steps {

        git([
                url: "https://github.com/srajunisum/springboot-dockerdemo.git",
                poll: true
            ])
     }
    }
    stage('Gradle Build') {
      steps{
          script{
                 bat 'gradlew.bat clean build'
          }
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage =  docker.build("ashokk16725/samedaydelivery")
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }

  }

}