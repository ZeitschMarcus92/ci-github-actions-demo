pipeline {
    agent any

    // 1. Globale Umgebungsvariablen
    environment {
        ENV = 'production'
        VERSION = '1.0.0'
        // Hinweis: Kein echtes Secret möglich – Dummy wird gesetzt
        MY_SECRET = 'DUMMY_SECRET_12345'
    }

    stages {
        stage('Global Variablen verwenden – Teil 1') {
            steps {
                echo "Stage 1: ENV = ${env.ENV}"
                echo "Stage 1: VERSION = ${env.VERSION}"
            }
        }

        // 2. Stage-spezifische Variable
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

        // 3. Secret (simuliert)
        stage('Simuliertes Secret') {
            steps {
                script {
                    def secret = env.MY_SECRET
                    echo "Simulierter Secret-Wert – Länge: ${secret.length()} Zeichen"
                }
            }
        }

        // 4. BONUS – Übergabe an Shell-Skript
        stage('BONUS: Shell-Skript') {
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
            echo "Pipeline erfolgreich abgeschlossen (Dummy-Version)"
        }
    }
}
