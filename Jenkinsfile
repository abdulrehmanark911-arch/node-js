#!groovy
pipeline {
    // Top-level par none hi rakhenge (Sir Noor ka standard)
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

        stage('Simulate Build & Test') {
            agent any
            steps {
                // Kyunki main controller par node nahi hai, hum echo se simulate karte hain real-world production flow ko
                echo '=== STEP 1: Code Checkout Kamyaab Hoa ==='
                echo '=== STEP 2: Pre-requisites Verified ==='
                echo '=== STEP 3: Production Options applied (Build Discarder & Timestamps active) ==='
                echo 'Agar Docker/Node plugin configured hota, toh actual testing yahan hoti.'
            }
            post {
                always {
                    cleanWs() // Workspace clean har haal mein hoga
                    echo 'Workspace clean up ho gaya successfully!'
                }
            }
        }
    }
}
