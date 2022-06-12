pipeline {
    
    agent {
        label "new_slave_pipeline"
    }
    
    
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
		sh "sudo docker build -t dockerimage:${BUILD_TAG} ."


		}
	}        
   
   }
    
    
}
