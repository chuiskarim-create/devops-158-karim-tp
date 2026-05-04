pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/chuiskarim-create/devops-158-karim-tp'
            }
        }
        stage('Build') {
            steps {
                sh 'docker build -t devops-158-karim .'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker stop devops-158-karim || true'
                sh 'docker rm devops-158-karim || true'
                sh 'docker run -d -p 5000:5000 --name devops-158-karim devops-158-karim'
            }
        }
    }
}
