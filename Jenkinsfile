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
        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker tag mytomcat $DOCKER_USER/mytomcat:latest
                        docker push $DOCKER_USER/mytomcat:latest
                        docker logout
                    '''
                }
            }
        }
                  
    }
}
