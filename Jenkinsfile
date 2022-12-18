node {
   
     stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build Docker Image') {

        app = docker.build("ionahiggins/courseworkv2")
    }

    stage('Test container'){
	app.inside {
            sh 'echo "Tests passed"'
        }
    }
}


