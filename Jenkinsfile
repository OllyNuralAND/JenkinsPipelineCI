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

            sh "ls"

           // sh "docker run -v /data:/data hashicorp/terraform:light plan main.tf"
            // sh "docker run -v /data:/data hashicorp/terraform:light plan data/main.tf"
            sh "docker run -v $(pwd):/app/ -w /app/ hashicorp/terraform:light init"
            sh "docker run -v $(pwd):/app/ -w /app/ hashicorp/terraform:light plan main.tf"
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