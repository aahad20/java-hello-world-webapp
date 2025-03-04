pipeline {
    agent any

    environment {
        TOMCAT_HOME = '/opt/tomcat'
        TOMCAT_USER = 'ec2-user'
        TOMCAT_PORT = '8080'
        EC2_IP = '3.14.128.92'
        GIT_REPO = 'https://github.com/aahad20/java-hello-world-webapp.git'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: "$GIT_REPO"
            }
        }
        
        stage('Build Java App') {
            steps {
                script {
                    // Maven build command (or Gradle depending on your setup)
                    sh 'mvn clean install'
                }
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                script {
                    sh """
                    scp target/your-java-app.war $TOMCAT_USER@$EC2_IP:$TOMCAT_HOME/webapps/
                    ssh $TOMCAT_USER@$EC2_IP "sudo systemctl restart tomcat"
                    """
                }
            }
        }
    }
}
