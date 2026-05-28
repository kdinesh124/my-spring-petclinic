pipeline {
    agent { label 'SPC'}
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('git Checkout') {
            steps {
                git url: "https://github.com/kdinesh124/my-spring-petclinic.git",
                branch: "main"
            }
        }
        stage('scan') {
            steps {
             withCredentials([string(credentialsId: 'sonar_id', variable: 'sonar')]) {
              withSonarQubeEnv('sonar') {
                sh """mvn clean verify sonar:sonar \
                       -Dsonar.projectkey=kdinesh124_my-spring-petclinic \
                       -Dsonar.organization=kdinesh124 \
                       -Dsonar.host.url=https://sonarcloud.io/ \
                       -Dsonar.login=$sonar"""
              }
        }
    }
  } 
}
}