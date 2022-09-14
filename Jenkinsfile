node {
    withDockerContainer(args: '-p 3000:3000', image: 'node:lts-bullseye-slim') {
        def BuiltSuccess = false

        stage('Built') {
            warnError('Error in build') {
                sh 'npm i'
            }
        }
        stage('Test') {
            if (BuiltSuccess == true) {
                warnError('Error in Test') {
                    sh './jenkins/scripts/test.sh'
                }
            }
        }
        stage('Post Action Clean UP WS') {
            cleanWs()
        }
    }
}