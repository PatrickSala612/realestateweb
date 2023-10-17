node ('ubuntu-appserver-cweb-2140') {
    def app
    stage('Cloning Git') {
        /* Lets make sure we have the repositroy cloned to our workspace */
        checkout scm
    }

    stage('Build-and-Tag') {
        /* This builds the actual image;
         * This is synonymous to docker build on the command line */
        app = docker.build("patrick612/realestateweb")
    }

    stage('Post-to-dockerhub') {
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials') {
            app.push("latest")
        }
    }

    stage('Pull-image-server') {
        sh "docker-compose down"
        sh "docker-compose up -d"
    }
}

