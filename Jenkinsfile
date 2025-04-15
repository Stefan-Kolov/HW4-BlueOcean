node {
    def app

    stage('Clone repository') {
        checkout scm
    }
    if (env.BRANCH_NAME == 'dev') {
        stage('Build image') {
            app = docker.build("stefankolov/hw4-blueocean")
        }
        stage('Push image') {
            docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                app.push("${env.BRANCH_NAME}-latest")
                // signal the orchestrator that there is a new version
            }
        }
    } else {
        echo "Skipping Docker build and push because branch is '${env.BRANCH_NAME}'"
    }
}
