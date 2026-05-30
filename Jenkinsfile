pipeline {
    agent { label 'SPCJAVA' }

    triggers {
        pollSCM('* * * * *')
    }

    stages {

        stage('Git Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/kdinesh124/my-spring-petclinic.git'
            }
        }

        stage('Sonar Scan') {
            steps {
                withCredentials([string(credentialsId: 'sonar_id', variable: 'SONAR_TOKEN')]) {
                    withSonarQubeEnv('SONAR') {
                        sh """
                            mvn clean verify sonar:sonar \
                            -Dsonar.projectKey=kdinesh124_my-spring-petclinic \
                            -Dsonar.organization=kdinesh124 \
                            -Dsonar.host.url=https://sonarcloud.io \
                            -Dsonar.token=${SONAR_TOKEN}
                        """
                    }
                }
            }
        }
            
        }
}