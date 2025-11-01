pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/Rafaelnascimento64/teste-jenkins.git'
        BRANCH = 'teste-jenkins-rafael'
    }

    stages {
        stage('Clonar repositório') {
            steps {
                git branch: "${BRANCH}", url: "${GIT_REPO}", credentialsId: 'a54577b0-4608-4b59-afdc-98314f10628a'
            }
        }

        stage('Verificar alterações') {
            steps {
                script {
                    // Verifica alterações locais
                    def changes = bat(script: "git status --porcelain", returnStdout: true).trim()
                    if (changes == '') {
                        echo "Nenhuma alteração detectada."
                        currentBuild.result = 'SUCCESS'
                        return
                    } else {
                        echo "Alterações encontradas:\n${changes}"
                    }
                }
            }
        }

        stage('Commit e Push') {
            steps {
                script {
                    // Executa comandos Git no Windows
                    bat """
                    git add .
                    git commit -m "Atualização automática via Jenkins" || echo Nada para commitar
                    git push origin %BRANCH%
                    """
                }
            }
        }
    }

    triggers {
        cron('H 8 * * *') // executa todo dia às 8h UTC
    }
}
