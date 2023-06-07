pipeline {
    
    agent any 
             stages {
                     stage('SCM') {
	               
                          steps {
			          git branch: 'main', url: 'https://github.com/ps103/jenkins_docker_pipline.git'
                                  
                                 }
            
                                 }
		      stage('Build by Maven Package') {
	                  
                          steps {
			         sh 'sudo mvn dependency:purge-local-repository'
                                 sh 'sudo mvn clean package'
                                }
            
                                                      }
                      stage('Deploy on testing') {
	                    agent {    
		                    label "slavenode"    
		                  }
	    
                          steps {
		                   sh 'pwd'
		                   sh 'sudo docker build -t java-repo:${BUILD_TAG} .'
				   sh 'sudo docker tag java-repo:$BUILD_TAG psharma10394/jenkins_docker_pipline:$BUILD_TAG'

	                	}
	                                                }
			}
	}		
               
