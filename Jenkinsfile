pipeline {

	agent any

	stages {
	
        stage('Stage-1 : Checkout Jenkins for React Github(repo)') {

          steps {          
                checkout scm
            }
            
        }        
		
	      stage('Stage-2 : Clone Github Spring Project') {
        
            steps {
                git branch: 'main', 
                credentialsId: 'github_token_aws_ec2',
                url: 'https://github.com/James-Lee/demo.git'
            }
            
            post {
            	success {
                    echo "Clone Github Spring Project Repository Successfully"
                }
                failure{
                    error 'Clone Github Spring Project Repository Failed'
                }
       		}
        }		        
    
					
		stage('Stage-3 : Gradle Build in Jenkins & make ROOT.war') {
		
			steps {							
				sh 'cd /var/jenkins_home/workspace/demo' 				
				sh 'pwd'
				sh 'ls -la'
				sh 'chmod +x gradlew'
				sh './gradlew clean build'
				sh 'ls -la ./build/libs'				
				sh 'pwd' 
				// sh 'cp build/libs/demo.war build/libs/ROOT.war' 
			}
			
			post {
				success {
                   echo 'Gradle Build & Copy Successfully'
                }
                failure{
                   error 'Gradle Build & Copy Failed'
                }
            }
		}
		
		stage('Stage-4 : Docker CP(Copy) From Jenkins To Tomcat & Tomcat Webapps Launching(Deployment)') {
		
			steps {
			    
				script {
				
				    sh 'docker cp /var/jenkins_home/workspace/demo/demo/build/libs/demo.war tomcat_10_1:/usr/local/tomcat/webapps'
				}

			}
		          
  		} //

	}
	
}
