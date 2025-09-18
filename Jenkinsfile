pipeline {
    agent {
        label 'master' // Assuming you have a Docker agent configured with this label
    }

    stages {
        stage('Build Maven App') {
            steps {
                script {
                    docker.image('maven:3.8.5-openjdk-17').inside {
                        sh 'git clone https://github.com/waypointcns/Multi-stage-multi-agent-' // Replace with your repo
                        dir('maven-hello-world') {
                            sh 'mvn clean package -DskipTests'
                            sh 'docker build -t my-maven-app .'
                        }
                    }
                }
            }
        }

        stage('Build Node.js App') {
            steps {
                script {
                    docker.image('node:18-alpine').inside {
                        sh 'git clone https://github.com/waypointcns/Multi-stage-multi-agent-' // Replace with your repo
                        dir('node-hello-world') {
                            sh 'npm install'
                            sh 'docker build -t my-node-app .'
                        }
                    }
                }
            }
        }

        stage('Run Docker Containers') {
            steps {
                sh 'docker run -d -p 8080:8080 --name maven-app my-maven-app'
                sh 'docker run -d -p 3000:3000 --name node-app my-node-app'
                // Add steps to verify applications are running, e.g., curl commands
            }
        }
    }

    post {
        always {
            sh 'docker stop maven-app || true'
            sh 'docker rm maven-app || true'
            sh 'docker stop node-app || true'
            sh 'docker rm node-app || true'
        }
    }
}
