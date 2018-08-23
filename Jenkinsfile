pipeline {
  agent {
    docker {
      alwaysPull true
      image 'alainchiasson/docker-molecule:develop'
      args '--privileged -v /DATA/docker-cache:/docker-cache'
    }
  }
  stages {
    stage ("Print out image env") {
      steps {
        // Jenkins check out the role into a folder with arbitrary name,
        // we need to let Ansible know where to find role
        sh 'env'
        sh 'mkdir -p molecule/default/roles'
        sh '[[ -e molecule/default/roles/simple ]] || ln -s `pwd` molecule/default/roles/simple'
      }
    }
    stage ("create.") {
      steps {
        sh 'molecule --debug create'
      }
    }
    stage ("converge.") {
      steps {
        sh 'molecule --debug converge'
      }
    }
    stage ("destroy") {
      steps {
        sh 'molecule --debug destroy'
      }
    }
  }
}
