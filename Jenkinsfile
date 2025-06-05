pipeline {
    agent any

    environment {
        ENV = 'production'
        VERSION = '1.0.0'
        MY_SECRET = credentials('MY_SECRET_CREDENTIAL')
    }

    stages {
        stage('Global Variablen verwenden – Teil 1') {
            steps {
                echo "Stage 1: ENV = ${env.ENV}"
                echo "Stage 1: VERSION = ${env.VERSION}"
            }
        }

        stage('Globale + lokale Variable – Teil 2') {
            environment {
                STAGE_ONLY = 'nur in dieser Stage'
            }
            steps {
                echo "Stage 2: ENV = ${env.ENV}"
                echo "Stage 2: VERSION = ${env.VERSION}"
                echo "Stage 2: STAGE_ONLY = ${env.STAGE_ONLY}"
            }
        }

        stage('Secrets verwenden – gefiltert') {
            steps {
                script {
                    def secret = env.MY_SECRET
                    echo "Geheimes Passwort wurde geladen. Länge: ${secret.length()} Zeichen"
                }
            }
        }

        stage('BONUS: Übergabe an Shell-Skript') {
            steps {
                writeFile file: 'myscript.sh', text: '''
                    #!/bin/bash
                    echo "Shell-Skript empfangen:"
                    echo "ENV: $1"
                    echo "VERSION: $2"
                '''
                sh 'chmod +x myscript.sh'
                sh './myscript.sh "$ENV" "$VERSION"'
            }
        }
    }

    post {
        always {
            echo "Pipeline fertig!"
        }
    }
}
