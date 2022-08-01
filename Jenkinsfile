node {
  def app
  stage('Clone repository') {
    checkout scm
  }

  stage('Update GIT') {
    script {
      catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
      withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
          //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8').
          sh "git config user.email tmpmalusr001@gmail.com"
          sh "git config user.name inalabs"
          //sh "git switch master"
          sh "cat deployment.yaml"
          // sed [options/flags...] [sed script] [input file(s)]
          // Change raj80dockerid with your dockerhub id
          // DOCKERTAG is a parameter defined in jenkins project later
          // it find the line inside the deployment.ymal and replace it
          sh "sed -i 's+democlouddevops/sfga-web.*+democlouddevops/sfga-web:${DOCKERTAG}+g' deployment.yaml"
          sh "cat deployment.yaml"
          sh "git add ."
          sh "git commit -m 'Commited by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
          sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/gitops_lb.git HEAD:main"
        }
      }
    }
  }
}





