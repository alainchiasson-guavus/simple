pipeline {
  agent {
    docker {
      alwaysPull true
      image 'alainchiasson/docker-molecule:latest'
      args '--privileged -v /DATA/docker-cache:/docker-cache'
    }
  }
  stages {
    stage ("Print out image env") {
      steps {
        sh 'env'
      }
    }
    stage ("create.") {
      steps {
        sh 'cd simple && molecule --debug create'
      }
    }
    stage ("converge.") {
      steps {
        sh 'cd simple && molecule --debug converge'
      }
    }
    stage ("destroy") {
      steps {
        sh 'cd simple && molecule --debug destroy'
      }
    }
  }
}
