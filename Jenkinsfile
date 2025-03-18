pipeline {
    agent any  // Run on any available Jenkins node
    
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-token',
                    url: 'https://github.com/Hemanthvarma1086263/devops-project.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'  // Build the project using Maven
            }
        }
        stage('Docker Build & Push') {
            steps {
                sh '''
                    docker build -t your-docker-image .
                    docker tag your-docker-image your-dockerhub-username/your-docker-image:latest
                    docker push your-dockerhub-username/your-docker-image:latest
                '''
            }
        }
        stage('Deploy to EC2') {
            steps {
                sh '''
                    docker run -d -p 8080:8080 your-dockerhub-username/your-docker-image:latest
                '''
            }
        }
    }
