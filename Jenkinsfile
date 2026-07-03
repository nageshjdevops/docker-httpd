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
                script {

                    if (env.BRANCH_NAME == "q1") {

                        sh '''
                        docker rm -f httpd-q1 || true
                        docker run -d --name httpd-q1 -p 8081:80 httpd
                        docker cp index.html httpd-q1:/usr/local/apache2/htdocs/index.html
                        '''

                    } else if (env.BRANCH_NAME == "q2") {

                        sh '''
                        docker rm -f httpd-q2 || true
                        docker run -d --name httpd-q2 -p 8082:80 httpd
                        docker cp index.html httpd-q2:/usr/local/apache2/htdocs/index.html
                        '''

                    } else if (env.BRANCH_NAME == "q3") {

                        sh '''
                        docker rm -f httpd-q3 || true
                        docker run -d --name httpd-q3 -p 8083:80 httpd
                        docker cp index.html httpd-q3:/usr/local/apache2/htdocs/index.html
                        '''

                    }

                }
            }
        }

    }
}

