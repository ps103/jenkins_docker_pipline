pipeline {
    
    agent {
        label "linuxbuildnode"
    }
    
    
    stages {
        stage('SCM') {
            steps {
                git 'https://github.com/vimallinuxworld13/jenkins-docker-maven-java-webapp.git'
                
            }
            
        }
        
        stage('Build by Maven Package') {
            steps {
                sh 'mvn clean package'
            }
            
        }
        
   }
    
    
}
