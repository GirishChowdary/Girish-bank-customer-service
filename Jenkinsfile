pipeline {
  agent any
  tools { 
       // maven 'Maven'
        jdk 'JAVA_HOME'
  }
  stages {
    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace... */
      steps {
        checkout scm
      }
    }
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
        sh 'echo $USER'
        sh 'echo whoami'
      }
    }
    stage('Docker Build') {
      steps {
        //sh '/usr/bin/docker build -t bank-customer-service .'
        sh '/usr/bin/docker build -t girish .'
      }
    }
    stage('Push image') {
      steps {
        withDockerRegistry([credentialsId: 'docker-hub', url: "https://index.docker.io/v1/"]) {
         sh  'docker tag bank-customer-service girish99/myfirsh:latest'
          sh '/usr/bin/docker push girish99/myfirsh:latest'
          
       // withDockerRegistry([credentialsId: 'us-east-2', url: "https://261167483116.dkr.ecr.us-east-2.amazonaws.com/girish"]) {
         // sh  'docker tag girish:latest 261167483116.dkr.ecr.us-east-2.amazonaws.com/girish:latest'
          //sh 'docker push 261167483116.dkr.ecr.us-east-2.amazonaws.com/girish:latest'          
        }
      }
    }
  }
}
