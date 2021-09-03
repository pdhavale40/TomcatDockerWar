node
{
def mavenHome = tool name: "Maven3.8.1"
    
    stage('checkout code')
    {
        git credentialsId: 'git_credential', url: 'https://github.com/pdhavale40/TomcatDockerWar.git'
    }
    stage('build')
    {
        sh "${mavenHome}/bin/mvn clean package"
    }
    stage('upload artifact into nexus')
    {
        sh "${mavenHome}/bin/mvn clean deploy"
    }
    stage('Execute SonarQube report')
    {
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    stage("Deploy to tomcat")
    {
        sshagent(['deploy_user']) 
        {
            sh "scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@54.255.120.128:/opt/apache-tomcat-8.5.68/webapps"
    
        }
    }
    stage('Email notification')
    {
        mail bcc: '', body: '''Build is success..
        
Regards,
Priyanka Dhavale''', cc: '', from: '', replyTo: '', subject: 'Build report', to: 'pdhavale40@gmail.com'
    }
}
    
