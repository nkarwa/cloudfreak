pipeline {
  agent any
    stages {      
        stage('Build maven ') {
            steps { 
                    sh 'pwd'      
                    sh '/opt/maven/maven/bin/mvn  clean install package'
            }
        }
        
        stage('Copy Artifact') {
           steps { 
                   sh 'pwd'
		   sh 'cp -r target/*.jar docker'
           }
        }
         
        stage('Build docker image') {
           steps {
               script {         
                 def customImage = docker.build('nkarwa/petclinic', "./docker")
                 docker.withRegistry('https://registry.hub.docker.com', 'docker_hub') {
                 customImage.push("${env.BUILD_NUMBER}")
                 }                     
           }
        }
	  }
    }
}
