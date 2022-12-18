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
   
    stage('Deploy Kubernetes Build'){
      sshagent(['my-ssh-key']) {
      sh  'ssh ubuntu@ec2-18-234-108-93.compute-1.amazonaws.com kubectl set image deployments/serverjsdeployment=docker.io/ionahiggins/courseworkv2:latest && ./multiple_users.sh'}
      }
  
}


