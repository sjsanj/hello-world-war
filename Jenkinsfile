pipeline{
	agent {label 'build'}
   
      stages{
     	 stage('Checkout external project') {
             steps {
		sh "rm -rf hello-world-war"
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
                    sh "docker build -t poovikas/tomcat:${BUILD_NUMBER} ."
         	 }
              }
          }
          stage('publish') {
              steps {
                 sh 'docker login --username=poovikas --password=Pooja@0108'
                 sh "docker push poovikas/tomcat:${BUILD_NUMBER}"
		 sh "helm package --version ${BUILD_NUMBER} helm/tomcat/ "
                 sh "curl -H \"X-JFrog-Art-Api:AKCp8nG69WYtBnNU9NKXJjGgazccbYAB9FicN8GkjKdgcCrg6pH3HGV1NWgLUJvpnB1kfde5q\" -T tomcat-${BUILD_NUMBER}.tgz \"https://helmpooj.jfrog.io/artifactory/helm_tomcat-helm/tomcat-${BUILD_NUMBER}.tgz\""
		
              }
         }
	 stage('deploy'){
             agent { label 'deployhelm' }
                steps{
                        sh "helm repo add helm_tomcat-helm https://helmpooj.jfrog.io/artifactory/api/helm/helm_tomcat-helm --username pooja.ab1994@gmail.com --password AKCp8nG69WYtBnNU9NKXJjGgazccbYAB9FicN8GkjKdgcCrg6pH3HGV1NWgLUJvpnB1kfde5q"
                        sh "helm repo update"
                        sh "helm upgrade --install tomcat helm_tomcat-helm/tomcat --set tag_name=${BUILD_NUMBER} --version ${BUILD_NUMBER}"
                 }
            }
 
       }
    }
