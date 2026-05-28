


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

                withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {

                    withSonarQubeEnv('SonarQube') {

                        sh '''
                        mvn clean verify sonar:sonar \
                        -Dsonar.projectKey=myproject \
                        -Dsonar.projectName=myproject \
                        -Dsonar.host.url=http://172.31.4.90:9000 \
                        -Dsonar.login=$SONAR_TOKEN
                        '''
                    }
                }
            }
        }
    }
}