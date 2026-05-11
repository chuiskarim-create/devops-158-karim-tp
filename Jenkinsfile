pipeline {
    agent any

    triggers {
        pollSCM('* * * * *') // vérifie toutes les minutes
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/chuiskarim-create/devops-158-karim-tp'
            }
        }

        stage('Pull latest code') {
            steps {
                sh '''
                    git config --global --add safe.directory /home/pi_158_karim/devops-158-karim-tp
                    cd /home/pi_158_karim/devops-158-karim-tp
                    git pull origin main
                '''
            }
        }

        stage('Install dependencies') {
            steps {
                sh '''
                    cd /home/pi_158_karim/devops-158-karim-tp
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install flask
                '''
            }
        }

        stage('Restart Flask app') {
            steps {
                sh '''
                    pkill -f "python app.py" || true
                    cd /home/pi_158_karim/devops-158-karim-tp
                    . venv/bin/activate
                    nohup python app.py > flask.log 2>&1 &
                '''
            }
        }
    }

    post {
        success {
            echo 'Déploiement automatique réussi ! BRAVO DAMN'
        }
        failure {
            echo 'Échec du pipeline. - AIE AIE AIE CA PUE'
        }
    }
}
