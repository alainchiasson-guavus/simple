pipeline {
  agent {
    docker {
      image 'docker:stable-dind'
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
      docker {
        image 'alainchiasson/docker-molecule'
      }
      steps {
        sh 'molecule --debug create'
      }
    }
    stage ("converge.") {
      docker {
        image 'alainchiasson/docker-molecule'
      }
      steps {
        sh 'molecule --debug converge'
      }
    }
    stage ("destroy") {
      docker {
        image 'alainchiasson/docker-molecule'
      }
      steps {
        sh 'molecule --debug destroy'
      }
    }
  }
}
