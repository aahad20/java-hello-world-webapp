pipeline {
    agent any

    environment {
        TOMCAT_USER = 'admin'   // Tomcat Username
        TOMCAT_PASS = 'Admin@123'    // Tomcat Password
        TOMCAT_URL = 'http://3.14.128.92:8080'  // Tomcat running on same EC2
        APP_NAME = 'login'  // Replace with your WAR app name
    }
    tools {
        maven 'm39'  // Name of Maven tool as configured in Jenkins

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/aahad20/java-hello-world-webapp.git'  // Public GitHub repo
            }
        }

        stage('Build with Maven') {
            steps {
                def mvnHome = tool name: 'm39', type: 'maven'
                                    sh "${mvnHome}/bin/mvn clean package"

            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh """
                curl -u $TOMCAT_USER:$TOMCAT_PASS -T target/${APP_NAME}.war $TOMCAT_URL/manager/text/deploy?path=/${APP_NAME}&update=true
                """
            }
        }
    }
}
