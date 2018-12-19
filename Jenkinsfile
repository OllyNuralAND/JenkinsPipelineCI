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

            sh "docker run hashicorp/terraform:light plan"
            // sh "docker run -i -t hashicorp/terraform:light apply main.tf"

            // docker.image("hashicorp/terraform").inside {
            //     // Run our Infrastructure as Code
            //     sh 'sh main.sh'
            // }
        }

        stage('Clean Up') {
            sh "docker ps -al"
            sh "docker rmi -f 'hashicorp/terraform'"
        }


    } catch (e) {
        throw e
    }
}