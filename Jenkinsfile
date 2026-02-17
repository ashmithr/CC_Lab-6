pipeline {
    agent any

    stages {

        stage('Build Backend Image') {
            steps {
                sh 'docker build -t backend-app backend'
            }
        }

        stage('Create Network') {
            steps {
                sh 'docker network create lab6-network || true'
            }
        }

        stage('Deploy Backends') {
            steps {
                sh '''
                docker rm -f backend1 backend2 || true
                docker run -d --network lab6-network --name backend1 backend-app
                docker run -d --network lab6-network --name backend2 backend-app
                sleep 3
                '''
            }
        }

        stage('Run NGINX') {
            steps {
                sh '''
                docker rm -f nginx-lb || true
                docker run -d \
                  --network lab6-network \
                  --name nginx-lb \
                  -p 80:80 \
                  -v $(pwd)/nginx/default.conf:/etc/nginx/conf.d/default.conf \
                  nginx
                sleep 3
                '''
            }
        }

    }
}