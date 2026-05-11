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
                sh 'cp -r $WORKSPACE/. /home/pi_158_karim/devops-158-karim-tp/'
            }
        }

        stage('Install dependencies') {
            steps {
                dir('/home/pi_158_karim/devops-158-karim-tp') {
                    sh '''
                        python3 -m venv venv
                        . venv/bin/activate
                        pip install flask
                    '''
                }
            }
        }

        stage('Restart Flask app') {
            steps {
                script {
                    sh 'pkill -f "python app.py" || true'
                    sh '''
                        cd /home/pi_158_karim/devops-158-karim-tp
                        . venv/bin/activate
                        nohup python app.py > flask.log 2>&1 &
                    '''
                }
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
