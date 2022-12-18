node {
   
     stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build Docker Image') {

        app = docker.build("ionahiggins/courseworkv2")
    }

    stage('Test Container'){
	app.inside {
            sh 'echo "Test to run a command within container passed."'
        }
    }
    stage('Push Image to DockerHub'){
         docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
    stage('Kubernetes Deployment'){
      sshagent(['my-ssh-key']) {
    sh kubectl set image deployments/serverjsdeployment serverjsdeployment=docker.io/ionahiggins/courseworkv2 && ./multiple_users.sh}
    }
}


