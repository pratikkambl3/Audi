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
				slackSend baseUrl: 'https://hooks.slack.com/services/', channel: '#audi', color: 'good', failOnError: false, message: 'Build is Successful', teamDomain: 'DEVOPS', tokenCredentialId: '1f1b4282-1076-4885-8ad1-96e2282535b7', username: 'SIRI'
				}
				}

		 stage("Failed-Notify"){
                        steps{
                                slackSend baseUrl: 'https://hooks.slack.com/services/', channel: '#audi', color: 'danger', failOnError: true, message: 'Build is Failed', teamDomain: 'DEVOPS', tokenCredentialId: '1f1b4282-1076-4885-8ad1-96e2282535b7', username: 'SIRI'}
                        }

		}


 }
