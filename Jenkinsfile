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
            docker.image("amazonlinux").inside {
                // Run our Infrastructure as Code
                sh 'sh dummy.sh'
                sh 'mvn clean install'
            }
        }

        stage('Clean Up') {
            sh "docker ps -al"
            sh "docker rmi -f 'amazonlinux'"
        }


    } catch (e) {
        throw e
    }
}