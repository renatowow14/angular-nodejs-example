 node {
    
    def SERVER_IP="192.168.25.13"

        stage('Checkout') {
            git branch: 'master',
            url: 'https://github.com/renatowow14/angular-nodejs-example.git'
        }
        stage('Validate') {
            echo "Validate Origin"
            sh 'git pull origin master'

        }
        stage('Build') {
            echo "Build application"
            sh "docker build -t nodejs-api -f Dockerfile . --no-cache" 
        }                               

        stage('Deploy') {
            echo "Deploy Application"
            sh "curl -v -X DELETE -s http://$SERVER_IP:4243/containers/nodejs-api?force=true"
            sh "curl -v -X POST -H 'Content-Type: application/json' -d @container.json -s http://$SERVER_IP:4243/containers/create?name=nodejs-api"
            sh "curl -v -X POST -s http://$SERVER_IP:4243/containers/nodejs-api/start"
        }    
 }
