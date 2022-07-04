pipeline { 
  agent any
  stages { 
    stage ('clone step'){
      steps {
        sh 'rm -rf hello-world-war'
      sh 'git clone https://github.com/PoojaVika/hello-world-war.git' }}
     stage ('build step'){
      steps {
        sh 'mvn package'}}
  stage ('deploy step'){
    steps { sh 'sudo cp /var/lib/jenkins/workspace/hello-word-war@2/target/hello-world-war-1.0.0.war /opt/apache-tomcat-9.0.64/webapps/' }}}}
