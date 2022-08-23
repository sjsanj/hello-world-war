pipeline{
      agent any
   
      stages{
     	 stage('Checkout external project') {
             steps {
            	sh "git clone https://github.com/PoojaVika/hello-world-war.git"
            	sh "ls -lat"
            	sh "pwd"
       	     }
          }
       	  stage('build'){
              steps{
                 dir('hello-world-war') {
		    sh "pwd"
	            sh "ls"
                    sh "echo ${BUILD_NUMBER}"
                    sh "sudo docker build -t poovikas/tomcat:${BUILD_NUMBER} ."
         	 }
              }
          }
          stage('publish') {
              steps {
                 sh 'sudo docker login --username=poovikas --password=Pooja@0108'
                 sh "sudo docker push poovikas/tomcat:${BUILD_NUMBER}"
		
              }
         }
 
       }
    }
