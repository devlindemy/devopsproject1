pipeline {
    agent any
	
	  tools
    {
       maven "MAVEN_HOME"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/devlindemy/devopsproject1.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t samplewebapp:latest .' 
                sh 'docker tag samplewebapp daemondocker01/samplewebapp:latest'
                //sh 'docker tag samplewebapp daemondocker01/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
          sh  'docker push daemondocker01/samplewebapp:latest'
        //  sh  'docker push daemondocker01/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 daemondocker01/samplewebapp"
 
            }
        }
// stage('Run Docker container on remote hosts') {
             
   //         steps {
     //           sh "docker -H ssh://jenkins@172.31.28.25 run -d -p 8003:8080 daemondocker01/samplewebapp"
 
    //        }
    //    }
    }
	}
    
