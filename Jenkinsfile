pipeline {
    agent any

    environment {
        TOMCAT_URL = 'http://3.14.128.92:8080'
        TOMCAT_APP = 'login'  // Name of your WAR file
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/your-repo.git'
            }
        }

        stage('Build Application') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'tomcat-credentials', usernameVariable: 'TOMCAT_USER', passwordVariable: 'TOMCAT_PASS')]) {
                    sh """
                    curl -u $TOMCAT_USER:$TOMCAT_PASS -T target/${TOMCAT_APP}.war $TOMCAT_URL/manager/text/deploy?path=/${TOMCAT_APP}&update=true
                    """
                }
            }
        }
    }
}
