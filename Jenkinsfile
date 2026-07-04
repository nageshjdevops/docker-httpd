pipeline {

    agent {
        label 'prod'
    }

    stages {

        stage('SCM') {
            steps {
                checkout scm
            }
        }

        stage('Pull HTTPD Image') {
            steps {
                sh 'docker pull httpd'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker rm -f httpd-q3 || true
                docker run -d --name httpd-q3 -p 8083:80 httpd
                docker cp index.html httpd-q3:/usr/local/apache2/htdocs/index.html
                docker exec httpd-q3 chmod 644 /usr/local/apache2/htdocs/index.html
                docker ps
                '''
            }
        }
    }

    post {
        success {
            echo 'PROD Deployment Successful'
        }
        failure {
            echo 'PROD Deployment Failed'
        }
    }
}
