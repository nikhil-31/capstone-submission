pipeline {

    agent any
    stages {
      
        stage('Cloning Git') {
            steps {
                checkout scm
            }
        }
        
        stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email nkl07ba@gmail.com"
                        sh "git config user.name Nikhil Bhaskar"
                        //sh "git switch master"
                        sh "cat deployment.yml"
                        sh "sed -i 's+raj80dockerid/test.*+raj80dockerid/test:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/django-docker-kubernetes-deploy-scripts.git HEAD:main"
                    }
                }
            }
        }

    }

}