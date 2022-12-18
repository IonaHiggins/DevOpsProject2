node {
    stage('Clone Github Repository') {
        script{
                git credentialsId: 'jenkins-user-github', url: 'https://github.com/aakashsehgal/FMU.git'
        }
    }

    stage('Build Docker Image') {

        app = docker.build("ionahiggins/courseworkv2")
    }

}


