node
{
def mavenHome = tool name: "Maven3.8.1"
    
    stage('checkout code')
    {
        git credentialsId: 'b5cbc4c0-6b60-4369-872b-2f62a5d494e9', url: 'https://github.com/pdhavale40/TomcatDockerWar.git'
        
    }
    stage('build')
    {
        sh "${mavenHome}/bin/mvn clean package"
    }
    stage('Execute SonarQube report')
    {
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    stage('upload artifact into nexus')
    {
        sh "${mavenHome}/bin/mvn clean deploy"
    }
    stage('Deploy to tomcat')
    {
        sshagent(['94de8363-6497-40aa-a535-86e91f6d4807'])
        {
            sh "scp -o StrictHostKeyChecking=no target/*.war ec2-user@ipaddress:/opt/tomcat/webapps"
        }
    }
    stage('Email notification')
    {
        mail bcc: '', body: '''Build is success..

Regards,
Priyanka Dhavale''', cc: '', from: '', replyTo: '', subject: 'Build report', to: 'pdhavale40@gmail.com'
    }
}
