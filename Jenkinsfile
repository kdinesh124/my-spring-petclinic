pipeline {
    agent any

    tools {
        maven 'maven'
        jdk 'jdk21'
    }

    environment {
        SONAR_TOKEN = credentials('sonar_id')
    }

    triggers {
        pollSCM('H/5 * * * *')
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/kdinesh124/my-spring-petclinic.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install -DskipTests'
            }
        }

        stage('SonarCloud Scan') {
            steps {
                withSonarQubeEnv('SonarCloud') {
                    sh """
                    mvn sonar:sonar \
                    -Dsonar.projectKey=kdinesh124_my-spring-petclinic \
                    -Dsonar.organization=kdinesh124 \
                    -Dsonar.host.url=https://sonarcloud.io \
                    -Dsonar.token=${SONAR_TOKEN}
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}