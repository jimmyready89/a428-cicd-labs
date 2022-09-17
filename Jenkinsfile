import org.jenkinsci.plugins.pipeline.modeldefinition.Utils

node {
    withDockerContainer(args: '-p 3000:3000', image: 'node:lts-bullseye-slim') {
        boolean PullSuccess = false
        boolean BuiltSuccess = false

        stage('cek tipe os') {
            if (isUnix() == false) {
                error "node harus berjalan di os unix"
            }
        }
        stage('Pull scripts dari repository github') {
            catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                git branch: 'react-app', url: 'https://github.com/jimmyready89/a428-cicd-labs'
                PullSuccess = true
            }
        }
        stage('Built') {
            if (PullSuccess == true) {
                catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                    sh 'npm i'
                    BuiltSuccess = true
                }
            }else{
                Utils.markStageSkippedForConditional(STAGE_NAME)
            }
        }
        stage('Menjalankan testing script') {
            if( BuiltSuccess == true ){
                catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                    sh './jenkins/scripts/test.sh'
                }
            }else{
                Utils.markStageSkippedForConditional(STAGE_NAME)
            }
        }
        stage('Post Action Clean UP WS') {
            if( BuiltSuccess == false ){
                cleanWs()
            }else{
                Utils.markStageSkippedForConditional(STAGE_NAME)
            }
        }
    }
}