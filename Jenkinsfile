pipeline{
    agent any
        triggers {
  pollSCM '* * * * *'
     }
     parameters {
  choice choices: ['QA', 'UAT', 'PROD'], name: 'ENV'
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
		stage("Failed-Notify"){
			steps{
				slackSend baseUrl: 'https://hooks.slack.com/services/', channel: '#audi', color: 'danger', failOnError: true, message: 'Build is Failed', teamDomain: 'DEVOPS', tokenCredentialId: 'Audi', username: 'SIRI'
				}
			}
		stage("Deployment"){
			steps{
   			sh '''if [ $ENV = "QA" ];then
cp target/Audi.war /home/vboxuser/Documents/DevopsTools/apache-tomcat-9.0.88/webapps
echo "Deployed to QA SERVER"
elif [ $ENV = "UAT" ];then
cp target/Audi.war /home/vboxuser/Documents/DevopsTools/apache-tomcat-9.0.88/webapps
echo "Deployed to UAT SERVER"
elif [ $ENV = "PROD" ];then
cp target/Audi.war /home/vboxuser/Documents/DevopsTools/apache-tomcat-9.0.88/webapps
echo "Deployed to PROD SERVER"
fi'''
					}
				}

		stage("Notification"){
			steps{
				slackSend baseUrl: 'https://hooks.slack.com/services/', channel: '#audi', color: 'good', message: 'Build is successful', teamDomain: 'DEVOPS', tokenCredentialId: 'Audi', username: 'SIRI'
				}
				}
		}


 }
