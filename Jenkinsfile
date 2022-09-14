node {
    withDockerContainer(args: '-p 3000:3000', image: 'node:lts-bullseye-slim') {
        def PullSuccess = false
        def BuiltSuccess = false

        stage('Pull scripts dari repository github') {
            catchError('Error in build') {
                git branch: 'react-app', url: 'https://github.com/jimmyready89/a428-cicd-labs'
                PullSuccess = true
            }
        }
        stage('Built') {
            if (PullSuccess) {
                catchError('Error in build') {
                    sh 'npm i'
                }
            }
        }
        stage('Test') {
            if (BuiltSuccess) {
                catchError('Error in Test') {
                    sh './jenkins/scripts/test.sh'
                }
            }
        }
        stage('Post Action Clean UP WS') {
            cleanWs()
        }
    }
}