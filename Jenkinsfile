node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email sanae.abahcine@esi.ac.ma"
                        sh "git config user.name sanaabahcine"
                        //sh "git switch master"
                        sh "cat deployementservice.yaml"
                        sh "sed -i 's+sanaeabahcine371/devops-integration.*+sanaeabahcine371/devops-integration:${DOCKERTAG}+g' deployementservice.yaml"
                        sh "cat deployementservice.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git HEAD:main"
      }
    }
  }
}
}
