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
        sh 'molecule --debug test'
      }
    }
    // stage ("converge.") {
    //   steps {
    //     sh 'molecule --debug converge'
    //   }
    // }
    // stage ("destroy") {
    //   steps {
    //     sh 'molecule --debug destroy'
    //   }
    // }
  }
}
