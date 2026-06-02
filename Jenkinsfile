#!groovy
pipeline {
    // Sir Noor ka 2026 production rule: top level par none rakha taake stages khud controller handle karein
    agent none

    options {
        buildDiscarder(logRotator(numToKeepStr: '5')) // Disk full hone se bachane ke liye (faqat 5 builds rakhega)
        disableConcurrentBuilds() // Do builds ko ek sath chal kar workspace tabaah karne se rokega
        timeout(time: 1, unit: 'HOURS') // Agar pipeline kahin phas jaye toh 1 hour mein automatically kill ho jaye
        timestamps() // Logs mein time dikhane ke liye (taake log easily samajh aayein)
    }

    stages {
        stage('Checkout Code') {
            agent any // Is stage ke liye koi bhi available worker server utha lo
            steps {
                checkout scm // Built-in checkout step, no manual git command!
            }
        }

        stage('Install Dependencies & Test') {
            agent any
            steps {
                // Kyun ke yeh container bilkul fresh hai, hum check karte hain node chal raha hai ya nahi
                sh 'node -v'
                sh 'npm -v'
                echo 'Dependencies install aur testing steps yahan hotay hain.'
            }
            post {
                always {
                    cleanWs() // Viva Point: Build pass ho ya fail, workspace ko bilkul saaf kar do!
                    echo 'Workspace successfully cleaned up!'
                }
            }
        }
    }
}
