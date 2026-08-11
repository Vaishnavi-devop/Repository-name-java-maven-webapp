pipeline {
    agent { label 'slave' }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh '''
                scp -o StrictHostKeyChecking=no target/java-maven-webapp.war ec2-user@172.31.27.146:/opt/tomcat/webapps/
                '''
            }
        }
    }

    post {
        success {
            echo 'Application Built and Deployed Successfully'
        }

        failure {
            echo 'Build or Deployment Failed'
        }
    }
}
