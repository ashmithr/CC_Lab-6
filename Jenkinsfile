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