node {
    try {
        stage('Clear Workspace') {
            step([$class: 'WsCleanup'])
        }

        stage('Pull') {
            checkout scm
        }

        stage('Build and Test') {
            sh 'docker run -v $(pwd):/app/ -v ${HOME}/.aws:/root/.aws -w /app/ hashicorp/terraform:light init'
            sh 'docker run -v $(pwd):/app/ -v ${HOME}/.aws:/root/.aws -w /app/ hashicorp/terraform:light validate'
            sh 'docker run -v $(pwd):/app/ -v ${HOME}/.aws:/root/.aws -w /app/ hashicorp/terraform:light plan'
        }

        stage('Clean Up') {
            sh "docker ps -al"
            sh "docker rmi -f 'hashicorp/terraform'"
        }
    } catch (e) {
        throw e
    }
}