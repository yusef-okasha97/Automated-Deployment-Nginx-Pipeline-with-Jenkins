pipeline {
    agent { label 'vm2' }  // Specify the agent label for VM2

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/yusef-okasha97/Automated-Deployment-Pipeline-with-Jenkins-and-Docker.git', branch: 'main', credentialsId: 'GitHub-Token'
            }
        }

        stage('Build Docker Images') {
            steps {
                script {
                    sh 'docker-compose -f docker-compose.yml build'
                }
            }
        }

        stage('Run Docker Compose on Localhost') {
            steps {
                script {
                    sh 'docker-compose -f docker-compose.yml up -d'
                }
            }
        }
    }

    post {
        always {
            script {
                sh 'docker-compose -f docker-compose.yml down'
                sh 'sudo rm -rf wordpress\ app/'
                sh 'sudo rm -rf wordpress\ app@tmp/'
            }
        }
    }
}
