pipeline {
    agent any

    environment {
        IMAGE = 'liliacr.azurecr.io/digitalex:v1.0.0'
    }

    stages {
        stage('Update GIT') {
            steps {
                script {
                    catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                        withCredentials([usernamePassword(credentialsId: 'karo-github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                            sh """
                            git config user.email "konissil@gmail.com"
                            git config user.name "lily4499"
                            git checkout main
                            sed -i 's#\\(image: \\).*#\\1${IMAGE}#' deployment.yml
                            git add deployment.yml
                            git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'
                            git push @github.com/${GIT_USERNAME}/argo-app-deploy-aks.git">https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/argo-app-deploy-aks.git HEAD:main
                            """
                        }
                    }
                }
            }
        }
    }
}
