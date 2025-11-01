pipeline {
    agent any

    environment {
        GIT_CREDENTIALS = 'https://github.com/ArtuTuin/teste-jenkins-arthur'
        BRANCH_NAME = 'teste-jenkins-arthur' 
    }

    triggers {
        cron('H 10 * * *')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: "${BRANCH_NAME}",
                    credentialsId: "${GIT_CREDENTIALS}",
                    url: 'https://github.com/ArtuTuin/teste-jenkins-arthur'
            }
        }

        stage('Verificar alterações') {
            steps {
                script {
                    sh '''
                    git fetch
                    if [ -n "$(git status --porcelain)" ]; then
                        echo "Há mudanças no repositório."
                        git add .
                        git commit -m "Atualização automática via Jenkins"
                        git push origin ${BRANCH_NAME}
                    else
                        echo "Nenhuma alteração detectada."
                    fi
                    '''
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline executada com sucesso."
        }
        failure {
            echo "Falha na execução da pipeline."
        }
    }
}
