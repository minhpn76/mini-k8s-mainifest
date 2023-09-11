pipeline{
  agent {
    node {
      label 'built-in'
    }
  }
  stages{
    stage("Change GIT deployment"){
      steps{
        script {
          catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
            withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
              //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
              sh "git config user.email phamngocminh7694@gmail.com"
              sh "git config user.name minhpn76"
              //sh "git switch master"
              sh "cat deployment.yaml"
              sh "sed -i 's+ghcr.io/minhpn76/mini-k8s-code.*+ghcr.io/minhpn76/mini-k8s-code:${DOCKERTAG}+g' deployment.yaml"
              sh "cat deployment.yaml"
              sh "git add ."
              sh "git commit -m 'Done by Jenkins Job changemanifest'"
              sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/mini-k8s-mainifest.git HEAD:main"
            }
          }
        }
      }
    }
  }
  post {
    success {
      echo "SUCCESSFUL"
    }
    failure {
      echo "FAILED"
    }
  }
}