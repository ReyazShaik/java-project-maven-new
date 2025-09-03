pipeline {
    agent any

    stages {
        stage('gitcheckout') {
            steps {
                git 'https://github.com/reddyhari3333-art/java-project-maven-new.git'
            }
        }
        stage('validate') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('dockerimage') {
            steps {
                sh 'docker rmi -f dockerimage || true'
                sh 'docker build -t dockerimage .'
                
                
                 sh 'docker rm -f c1 || true'
                sh 'docker run -itd --name c1 -p 8888:8080 dockerimage'
            }
        }
        stage('docker push'){
            steps {
                docker.withRegistry('https://index.docker.io/v1/', 'docker-hub-credentials') {
                    def app =
                docker.build("harireddy2910/hotstar-app:${env.BUILD_NUMBER}")
                    app.push()
               }
           }
    }
}
