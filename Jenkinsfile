pipeline {
    
    agent any
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', credentialsId: 'Git', url: 'https://github.com/Sandeep-HN/ai-leads.git'
            }
        }
        stage('Maven Build'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('Tomcat Deploy -Dev'){
            steps{
                sshagent(['tomcat-dev']) {
                    // copy war file to tomcat
                   sh 'scp -o StrictHostKeyChecking=no target/ai-leads.war ec2-user@172.31.47.174:/opt/tomcat/webapps'
                   sh 'ssh ec2-user@172.31.47.174 /opt/tomcat/bin/shutdown.sh'
                   sh 'ssh ec2-user@172.31.47.174 /opt/tomcat/bin/startup.sh'
                }
            }
        }
    }
}
