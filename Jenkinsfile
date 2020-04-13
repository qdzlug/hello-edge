node {
    def app

    stage('Clone repository') {
        /* 
         * Let's make sure we have the repository
         * cloned to our workspace 
         */

        checkout scm
    }

    stage('Build image') {
        /*
         * This builds the actual image; synonymous to
         * docker build on the command line 
         */

        app = docker.build("demoorg/images/test")
    }

    stage('Test image') {
        /*
         *  Ideally, we would run a test framework against our image.
         */ 

        app.inside {
            sh 'hostname'
        }
    }

    stage('Push image') {
        /*
         * Finally, we'll push the image with two tags:
         * First, a hardcoded version number; we could use
         * the jenkins build if we wanted.
         * 
         * Second, the 'latest' tag.
         *
         * Note how we refer to the build in terms of tags;
         * this is how we make sure we can upload to the MeX
         * registry.
         */
        docker.withRegistry('https://docker.mobiledgex.net/demoorg/images', 'MeX-Demo') {
            app.push("${env:1.1}")
            app.push("latest")
        }
    }
}
