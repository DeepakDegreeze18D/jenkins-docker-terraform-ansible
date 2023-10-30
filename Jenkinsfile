pipeline {
  agent any
  stages {
    stage('Compile') {
      steps {
        script{
                def mvnHome = tool name: 'MAVEN_HOME', type: 'maven'
                sh "${mvnHome}/bin/mvn package"
                sh 'mv target/myweb*.war target/newapp.war'
        }
      }
    }
    stage('Building Docker Image') {
      steps{
        script {
          sh "docker build -t deepakdegreeze/myweb:0.0.2 ."
        }
      }
    }
    stage('Push Image To Docker Hub') {
      steps{
        script {
          sh "echo $USER"
          sh "docker login -u deepakdegreeze -p kdeepak18d"
          sh "docker push deepakdegreeze/myweb:0.0.2 ."
          }
        }
      }
    stage('Docker deployment'){
      steps{
        script {
          sh 'docker run -d -p 8090:8080 --name tomcattest deepakdegreeze/myweb:0.0.2 .' 
          }
        }
      }
    }
}
