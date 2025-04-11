pipeline {
    agent any

    environment {
        DEPLOY_DIR = "/var/www/pikniknow-web"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git credentialsId: 'github-credentials', url: 'https://github.com/Angad0691996/pikniknow-web..git', branch: 'main'
            }
        }

        stage('Deploy Website') {
            steps {
                script {
                    sh """
                        echo "Clearing old site..."
                        sudo rm -rf \$DEPLOY_DIR/*
                        
                        echo "Deploying new site..."
                        sudo cp -r * \$DEPLOY_DIR/
                        sudo chown -R www-data:www-data \$DEPLOY_DIR
                    """
                }
            }
        }

        stage('Restart Nginx') {
            steps {
                script {
                    sh "sudo systemctl restart nginx"
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
