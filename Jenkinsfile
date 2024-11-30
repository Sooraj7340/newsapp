pipeline{
    agent any

    stages{
        stage('Verify Git') {
            steps {
                sh 'git --version'
            }
        }
        stage('Git Checkout'){
            steps{
                git branch: 'dev', url: 'https://github.com/Sooraj7340/newsapp.git'
            }
        }
        stage('Docker Build'){
            steps{
                sh "docker build -t suraj7340/one9:1"
            }
        }
        stage('Containerisation'){
            steps{
                sh '''
            docker stop c1
            docker rm c1
            docker run -d --name c1 -p 3000:3000 suraj7340/one9:1
            '''
            }
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