pipeline {
    agent { label 'master' }
    parameters {
        string(name: 'jfrog_user', defaultValue: '', description: ' this is user name for jfrog') 
        string(name: 'jfrog_pass', defaultValue: '', description: ' this is password for jfrog')
    }
    environment {
        env.http_user = "${params.jfrog_user}"
        env.http_password = "${params.jfrog_pass}"
    } 
    stages {
        stage('build code and push code to artifact jfrog repo ') {
            steps {
                sh "cd java-war-project-feature-cicd && mvn clean deploy"
            }
        }
    
        stage('deployment on tomcat') {
            steps {
                sh """
                    wget --http-user=${env.http_user} --http-password=${env.http_password} https://satishloka4666.jfrog.io/artifactory/com/mycompany/app/my-app-lokasatish/2.0/my-app-lokasatish-2.0.war
                    mv my-app-lokasatish-2.0.war   my-app-satish.war
                    cp my-app-satish.war /home/satish/tomcat9/webapps
                """
            }
        }
    }
}
