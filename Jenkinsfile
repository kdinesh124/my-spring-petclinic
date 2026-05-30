pipeline {
    agent any

    stages {

        stage('Git Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/kdinesh124/my-spring-petclinic.git'
            }
        }

        stage('Build & Sonar Scan') {
            steps {

                withCredentials([string(credentialsId: 'sonar_id', variable: 'SONAR_TOKEN')]) {

                    withSonarQubeEnv('SonarQube') {

                        sh '''
                        mvn clean verify sonar:sonar \
                        -Dsonar.projectKey=myproject \
                        -Dsonar.projectName=myproject \
                        -Dsonar.host.url=https://sonarcloud.io/ \
                        -Dsonar.login=$SONAR_TOKEN
                        '''
                    }
                }
            }
        }
    }
}