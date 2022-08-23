pipeline{
	agent {label 'build'}
   
      stages{
     	 stage('Checkout external project') {
             steps {
		sh "rm -rf hello-world-war"
            	sh "git clone https://github.com/sjsanj/hello-world-war.git"
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
                    sh "docker build -t sanjsj/samplewebapp:${BUILD_NUMBER} ."
         	 }
              }
          }
          stage('publish') {
              steps {
                 sh 'docker login --username=sanjsj --password=sanju@123'
                 sh "docker push sanjsj/samplewebapp:${BUILD_NUMBER}"
		 sh "helm package --version ${BUILD_NUMBER} helm/tomcat/ "
                 sh "curl -H \"X-JFrog-Art-Api:AKCp8nG69Y15qxFN173x5XFCBkEr6aLaRQyMkhYnmBZTYVaiYMK7eCBoFWd86k7SL285cPKdP\" -T tomcat-${BUILD_NUMBER}.tgz \"https://helmsanj.jfrog.io/artifactory/helm_tomcat-helm/tomcat-${BUILD_NUMBER}.tgz\""
		
              }
         
	 
                 }
            }
 
       }
    }
