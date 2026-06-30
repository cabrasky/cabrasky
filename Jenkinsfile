pipeline {
    agent any

    triggers {
        pollSCM('* * * * *')
    }

    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }

    environment {
        DEPLOY_DIR = '/var/www/cabrasky'
    }

    stages {
        stage('Deploy to nginx') {
            steps {
                sh """
                    cp index.html "${DEPLOY_DIR}/"
                    cp favicon.svg "${DEPLOY_DIR}/" 2>/dev/null || true
                """
            }
        }
    }

    post {
        success {
            echo '✅ www.cabrasky.net deployed successfully'
        }
        failure {
            echo '❌ Deploy failed'
        }
    }
}
