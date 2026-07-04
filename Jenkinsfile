pipeline {

    agent any

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
                docker rm -f httpd-q2 || true
                docker run -d --name httpd-q2 -p 8082:80 httpd
                docker cp index.html httpd-q2:/usr/local/apache2/htdocs/index.html
                docker exec httpd-q2 chmod 644 /usr/local/apache2/htdocs/index.html
                docker ps
                '''
            }
        }

    }

    post {
        success {
            echo 'Deployment Successful'
        }
        failure {
            echo 'Deployment Failed'
        }
    }
}
