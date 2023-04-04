pipeline {
  agent { label 'master' }
  parameters { string(name: 'jfrog_user', defaultValue: '', description: ' this is user name for jfrog') 
               string(name: 'jfrog_pass', defaultValue: '', description: ' this is password for jfrog') }
  environment {
                http-user = "jfrog_user"
	        http-password = "jfrog_pass"
                     
            }
  
  stages {
    stage('build code and push code to artifact repo ') {
      steps {
        sh "cd java-war-project-feature-cicd && mvn clean deploy"
      }
    }
    
    stage('deployment on tomcat') {
      steps {
        sh """
             wget --http-user=${jfrog_user}  --http-password=${jfrog_pass} https://satishloka4666.jfrog.io/artifactory/com/mycompany/app/my-app-lokasatish/2.0/my-app-lokasatish-2.0.war
	     mv my-app-lokasatish-2.0.war   my-app-satish.war
             cp my-app-satish.war /home/satish/tomcat9/webapps
          """
      }
    }
  }
  }
