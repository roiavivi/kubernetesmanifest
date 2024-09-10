pipeline {

  agent {
    kubernetes {
      yamlFile 'DeploymentPod.yaml'
    }
  }
  stages {
    stage('Test image') {
	    steps {
		sh 'git --version'
	    }
    }
    }
  }
}
