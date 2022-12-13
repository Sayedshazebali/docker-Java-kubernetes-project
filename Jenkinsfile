pipeline {
    agent any
    tools {nodejs "node16" }
    environment {
        NODE_ENV='production'
    }
    
  
    stages {
        stage('source') {
            steps {
               git 'https://github.com/Sayedshazebali/docker-Java-kubernetes-project.git'
               
            }
            
        }
	agent none  stages {
  	stage('Maven Install') {
    	agent {
      	docker {
        	image 'maven:3.5.0'
        }
      steps {
      	sh 'mvn clean install'
      }
    }
    stage('Docker Build') {
    	agent any
      steps {
      	sh 'docker build -t shazebali7/productcatlogue:latest .'
      }
    }
    stage('Docker Push') {
    	agent any
      steps {
      	withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
        	sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh 'docker push shazebali7/productcatlogue:latest'
        }
      }
    }
  }
}
