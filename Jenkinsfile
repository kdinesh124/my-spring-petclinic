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
              withSonarQubeEnv('sonar') {
                sh "mvn package sonar:sonar"
            }
        }
    }
}
}