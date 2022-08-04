pipeline {
    agent any	
	 
 stages {
      stage('checkout') {
           steps {             
                git branch: 'master', url: 'https://github.com/DGMalli/hello-world-war.git'             
          }
        }       

  stage('Docker Build and Tag') {
           steps {  
		 
                sh 'sudo docker build -t hello:v1 .' 
                sh 'sudo docker tag hello poovikas/hello:v1' 
            }
        }

stage('Login to Docker hub') {
           steps {
              
                sh 'sudo docker login --username=poovikas --password=Pooja@0108'
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
       	  sh  'sudo docker push poovikas/hello:v1'  
        }                 
          
        }     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
	      {
                sh "sudo docker run -d -p 8888:8080 poovikas/hello:v1"
             }
        }
 
    }
	}
