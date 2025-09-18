pipeline {
    agent any // Or a specific agent for the Jenkins server itself

    stages {
        stage('Maven Application Build and Test') {
            agent {
                docker { image 'maven:3.8.5-jdk-11' }
            }
            steps {
                dir('maven-app') { // Assuming your Maven app is in a 'maven-app' subdirectory
                    sh 'mvn clean install'
                    sh 'mvn test'
                }
            }
        }

        stage('Node.js Application Build and Test') {
            agent {
                docker { image 'node:16-alpine' }
            }
            steps {
                dir('nodejs-app') { // Assuming your Node.js app is in a 'nodejs-app' subdirectory
                    sh 'npm install'
                    sh 'npm test'
                }
            }
        }
        // Add more common stages or specific deployment stages here
    }
}
