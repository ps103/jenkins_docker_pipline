pipeline {
    
    agent any 
             stages {
                     stage('SCM') {
	                    agent {
	    	                   label "slavenode"
		            } 
                          steps {
			          git 'https://github.com/ps103/maven_java.git'
                                  
                                 }
            
                                 }
		      stage('Build by Maven Package') {
	                    agent {    
		                    label "slavenode"    
		                  } 
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
				   sh 'sudo docker tag java-repo:$BUILD_TAG psharma10394/maven_java:$BUILD_TAG'

	                	}
	                                                }
			}
	}		
               
