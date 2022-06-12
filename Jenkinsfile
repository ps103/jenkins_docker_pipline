pipeline {
    
    agent any 
    stages {
        stage('SCM') {
            steps {
                git 'https://github.com/sr98877/pipeline-code.git'
            }
            
        }
        
        stage('Build by Maven Package') {
            steps {
                sh 'mvn clean package'
            }
            
        }
        stage('Deploy on testing') {
            steps {
		// sh 'pwd'
		sh "sudo docker build -t srronak/javatest-app:${BUILD_TAG} ."
		}
	}        
        stage('Pushing image to docker hub') {
	    agent {    
		label "docker-slave"
		}
            steps {
	        withCredentials([string(credentialsId: 'Docker_hub_passwd', variable: 'Docker_hub_passwd_var')]) {

		sh "sudo docker login -u srronak -p ${Docker_hub_passwd_var}"
		}
		//sh "sudo docker push srronak/javatest-app:${BUILD_TAG}"

	}        
   
      }
      stage('Deploy on Docker Container') {
      	agent {
		label "docker-slave"
		}
	steps {
	
		sh "sudo ocker run -dit --name web1 -p 8080 srronak/javatest-app:${BUILD_TAG}"
		}

	}
   }
    
}

