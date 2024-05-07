pipeline{
    agent any
        triggers {
  pollSCM '* * * * *'
     }
    
   	stages{
	 	stage("Checkout SCM"){
			steps{
				checkout scm
				}
			}
   		stage("Building"){
			steps{
			sh'/home/vboxuser/Documents/DevopsTools/apache-maven-3.9.6/bin/mvn install' 
				}
			}

		stage("Deployment"){
			steps{
				sh'cp target/Audi.war /home/vboxuser/Documents/DevopsTools/apache-tomcat-9.0.88/webapps'
					}
				}
		}


 }
