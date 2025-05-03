pipeline {
    agent any
    environment {
        IMAGE_NAME = "mukesh2007pandey/devops-demo:${GIT_COMMIT}"
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/mukesh2007pandey/devops-pipeline-demo.git'
            }
        }
        stage('Build Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
        stage('Push Image') {
            steps {
                withCredentials([string(credentialsId: 'Ericsson@123', variable: 'DOCKER_PASS')]) {
                    sh '''
                        echo $DOCKER_PASS | docker login -u mukesh2007pandey --password-stdin
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
