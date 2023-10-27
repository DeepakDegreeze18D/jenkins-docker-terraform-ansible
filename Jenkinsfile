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
          sh "docker build -t deepakdegreeze/cicd-poc-jenkins-ansible:$BUILD_NUMBER ."
        }
      }
    }
    stage('Push Image To Docker Hub') {
      steps{
        script {
          sh "echo $USER"
          sh "docker login -u deepakdegreeze -p kdeepak18d"
          sh "docker push deepakdegreeze/cicd-poc-jenkins-ansible:$BUILD_NUMBER"
          }
        }
      }
    stage('Docker deployment'){
    sh 'docker run -d -p 8090:8080 --name tomcattest deepakdegreeze/cicd-poc-jenkins-ansible:$BUILD_NUMBER' 
    }
    }
}

