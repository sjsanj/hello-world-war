pipeline {
    agent any
 
 stages {
      stage('checkout') {
           steps {
                  git branch: 'master', url: 'https://github.com/PoojaVika/hello-world-war.git'
             }
        }
	 
        stage('Docker Build and Tag') {
           steps {
                sh 'sudo docker build -t cicd .' 
                sh 'sudo docker tag docker_icicd Poovikas/cicd:latest'  
          }
        }
		
		stage('docker login') {
			steps{
			sh 'sudo docker login --username=PooVikas --password=Pooja@0108'
			}
		}
        stage('Publish image to Docker Hub') {
          
            steps {
                  sh 'sudo docker push PooVikas/cicd:latest'
                  
          }
        }
     
        stage('Run Docker Deploy') {
             
            steps {
                sh 'sudo docker run -d -p 8888:8080 PooVikas/cicd:latest'
 
            }
        }
    }
 }
