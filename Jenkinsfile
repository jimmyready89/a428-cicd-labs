node {
    withDockerContainer(args: '-p 3000:3000', image: 'node:lts-bullseye-slim') {
        def PullSuccess = false
        def BuiltSuccess = false

        stage('Pull scripts dari repository github') {
            catchError(message: 'Errro in build') {
                git branch: 'react-app', url: 'https://github.com/jimmyready89/a428-cicd-labs'
                PullSuccess = true
            }
        }
        stage('Built') {
            if (PullSuccess) {
                catchError(message: 'Error in build') {
                    sh 'npm i'
                    BuiltSuccess = true
                }
            }
        }
        stage('Test') {
            if (BuiltSuccess) {
                catchError(message: 'Error in Test') {
                    sh './jenkins/scripts/test.sh'
                }
            }
        }
        stage('Post Action Clean UP WS') {
            cleanWs()
        }
    }
}