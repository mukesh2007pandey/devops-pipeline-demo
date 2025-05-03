pipeline {
    agent any
    environment {
        IMAGE_NAME = "yourdockerhubuser/devops-demo:${GIT_COMMIT}"
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/yourusername/devops-pipeline-demo.git'
            }
        }
        stage('Build Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
        stage('Push Image') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-password', variable: 'DOCKER_PASS')]) {
                    sh '''
                        echo $DOCKER_PASS | docker login -u yourdockerhubuser --password-stdin
                        docker push $IMAGE_NAME
                    '''
                }
            }
        }
        stage('Deploy with Ansible') {
            steps {
                sh 'ansible-playbook -i ansible/inventory ansible/deploy.yml -e "image_tag=${GIT_COMMIT}"'
            }
        }
    }
}
