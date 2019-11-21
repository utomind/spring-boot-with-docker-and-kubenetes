pipeline {
  environment {
    registryCredential = 'docker-credentials'
    dockerImage = ''
  }
  agent any

  stages {
    stage('Cloning Git') {
      steps {

        git([
                url: "https://github.com/k-ashok/spring-boot-1.git",
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
          dockerImage =  docker.build("ashokk16725/samedaydelivery:1")
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
      stage('deploy App') {
         steps{
            script {
                kubernetesDeploy(configs:"dockerkubernate.yaml",kubeconfigId:"mykubeconfig")
            }
         }
        }
  }
}