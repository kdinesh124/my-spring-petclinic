pipeline {
    agent { label 'SPCJAVA' }
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('git checkout') {
            step {
                git url: 'https://github.com/kdinesh124/my-spring-petclinic.git',
                branch: "main"
            }
        }
        stage('scan') {
            steps {
             withCredentials([string(credentialsId: 'sonar_id', variable: ;SONAR_TOKEN)]) {
              withSonarQubeEnv('SONAR') {
                sh """mvn clear verify sonar:sonar \
                      -Dsonar.projectkey=kdinesh124_my-spring-petclinic \
                      -Dsonar.organization=kdinesh124 \
                      -Dsonar.host.url=https://sonarcloud.io/ \
                      -Dsonar.login=${SONAR+TOKEN}"""
              }
             }

            }
        }
    }
}







