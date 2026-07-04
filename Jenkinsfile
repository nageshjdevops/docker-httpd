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
                docker rm -f httpd-q1 || true
                docker run -d --name httpd-q1 -p 8081:80 httpd
                docker cp index.html httpd-q1:/usr/local/apache2/htdocs/index.html
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
