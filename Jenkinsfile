pipeline {
  agent any
  stages {
    stage('Compile') {
      steps {
        script{
                def mvnHome = tool name: 'MAVEN_HOME', type: 'maven'
                sh "${mvnHome}/bin/mvn package"
        }
      }
    }
    stage('Building Docker Image') {
      steps{
        script {
          sh "docker build -t cicd-poc-jenkins-ansible:$BUILD_NUMBER ."
        }
      }
    }
    stage('Push Image To Docker Hub') {
      steps{
        script {
          sh "echo $USER"
          sh "docker login -u deepakdegreeze -p kdeepak18d"
          sh "docker push cicd-poc-jenkins-ansible:$BUILD_NUMBER ."
          }
        }
      }
    stage('Docker deployment'){
      steps{
        script {
          sh 'docker run -d -p 8090:8080 --name tomcattest cicd-poc-jenkins-ansible:$BUILD_NUMBER .' 
          }
        }
      }
    }
}
