pipeline{
    agent any

    stages{
        stage('Git Checkout'){
            git branch: 'dev', url: 'https://github.com/Sooraj7340/newsapp.git'
        }
        stage('Docker Build'){
            sh "docker build -t suraj7340/one9:1"
        }
        stage('Containerisation'){
            sh '''
            docker stop c1
            docker rm c1
            docker run -d --name c1 -p 3000:3000 suraj7340/one9:1
            '''
        }
        stage('Login to Docker Hub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh "echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin"
                    }
                }
            }
        }

        stage('Pushing image to repository'){
            steps{
                sh 'docker push suraj7340/one9:1'
            }
        }

    }
}