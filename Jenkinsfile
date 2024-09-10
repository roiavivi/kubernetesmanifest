pipeline {
  agent {
    kubernetes {
      yamlFile 'DeploymentPod.yaml'
    }
  }
  stages {
    stage('Update GIT') {
      script {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
          withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
            sh "git config user.email 'roie710@gmail.com'"
            sh "git config user.name 'roie710'"
            sh "cat deployment.yaml"
            sh "sed -i 's+roie710/flask.*+roie710/flask:${DOCKERTAG}+g' deployment.yaml"
            sh "cat deployment.yaml"
            sh "git add ."
            sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
            sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git HEAD:main"
          }
        }
      }
    }
  }
}
