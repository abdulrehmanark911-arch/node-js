#!groovy
pipeline {
    agent none

    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
        disableConcurrentBuilds()
        timeout(time: 1, unit: 'HOURS')
        timestamps()
    }

    stages {
        stage('Checkout Code') {
            agent any
            steps {
                checkout scm
            }
        }

        stage('Install & Test inside Docker') {
            // Yahan hum Jenkins ko bol rahe hain ke Node 20 ka container lekar aao!
            agent {
                docker {
                    image 'node:20-alpine'
                }
            }
            steps {
                // Ab yeh commands Jenkins ke upar nahi, balkay is container ke andar chalengi jahan Node pehle se hai!
                sh 'node -v'
                sh 'npm -v'
                echo 'Docker agent ke andar Node.js ekdum makhhan chal raha hai!'
            }
            post {
                always {
                    cleanWs()
                    echo 'Workspace cleaned!'
                }
            }
        }
    }
}
