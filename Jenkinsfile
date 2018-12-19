node {
    try {
        stage('Clear Workspace') {
            step([$class: 'WsCleanup'])
        }

        stage('Pull') {
            checkout scm
        }

        stage('Build and Test') {
            // Exec into Docker image containing Terraform
            docker.image("hashicorp/terraform").inside {
                // Run our Infrastructure as Code
                sh 'sh dummy.sh'
            }
        }

        stage('Clean Up') {
            sh "docker ps -al"
            sh "docker rmi -f 'hashicorp/terraform'"
        }


    } catch (e) {
        throw e
    }
}