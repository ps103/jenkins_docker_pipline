pipeline {
    
    agent any 
    stages {
        stage('SCM') {
	    agent {
	    	label "pipeline"
		}
            steps {
                git 'https://github.com/sr98877/pipeline-code.git'
            }
            
        }
        
        stage('Build by Maven Package') {
	    agent {    
		label "pipeline"    
		}
            steps {
                sh 'mvn clean package'
            }
            
        }
        /*stage('Deploy on testing') {
	    agent {    
		label "pipeline"    
		}
	    
            steps {
		// sh 'pwd'
		 sh "sudo docker build -t srronak/javatest-app:${BUILD_TAG} ."
		}
	} */       
        stage('Pushing image to docker hub') {
	    agent {    
		label "pipeline"    
		}
            steps {
	        withCredentials([string(credentialsId: 'docker_hub_passwd', variable: 'Docker_hub_passwd_var')]) {

		sh "sudo docker login -u srronak -p ${docker_hub_passwd_var}"
		}
		//sh "sudo docker push srronak/javatest-app:${BUILD_TAG}"

	}        
   
      }
      stage('Deploy on Docker Container') {
      	agent {
		label "pipeline"    
		}
	steps {
		sh "sudo docker pull srronak/javatest-app:jenkins-pipeline-code-17"
		sh "sudo docker run -dit --name web1 -p 8080 srronak/javatest-app:jenkins-pipeline-code-17"
		}

	}
	stage('QAT testing') {
	agent { 
		label "pipeline"
		}
	steps {
		retry(5) {
		sh "curl --silent http://35.154.193.35:49153/java-web-app | grep -iname zeetron"
		}
	   }
	}

	stage("Approval status") {
		agent {
			label "pipeline1"
			}
		steps {
		script {
			Boolean user_input = input(id: 'Process1', message: 'Enter your confirmation')
			echo "user input : ${user_input}"
			}
		}
	}
      stage('Deploy on Docker Container on Prod Env') {
      	agent {
		label "pipeline2"    
		}
	steps {
		sh "sudo docker pull srronak/javatest-app:jenkins-pipeline-code-17"
		sh "sudo docker run -dit --name web1 -p 8080 srronak/javatest-app:jenkins-pipeline-code-17"
		}

	}
   }
    
}

