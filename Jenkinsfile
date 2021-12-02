node {
    def app

    stage('check out') {
        checkout scm
    }

    stage('Build image') {
        app = docker.build("josephhodespipeline.azurecr.io/hellonode")
    }

    stage('Test image') {
        app.inside {
            sh 'node test.js'
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        docker.withRegistry('https://josephhodespipeline.azurecr.io') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
