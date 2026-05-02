pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME'   // Configure in Jenkins → Global Tool Configuration
        jdk 'JDK11'
    }

    environment {
        TOMCAT_URL    = 'http://localhost:8080'      // Change to your Tomcat URL
        TOMCAT_CRED   = 'tomcat-deployer'            // Jenkins credentials ID
        WAR_FILE      = 'target/book-appointment.war'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/<your-username>/book-appointment.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [
                    tomcat9(
                        credentialsId: "${TOMCAT_CRED}",
                        url: "${TOMCAT_URL}",
                        path: '/book-appointment'
                    )
                ],
                contextPath: '/book-appointment',
                war: "${WAR_FILE}"
            }
        }
    }

    post {
        success {
            echo "✅ Deployed: ${TOMCAT_URL}/book-appointment/"
        }
        failure {
            echo '❌ Build/Deploy failed.'
        }
    }
}