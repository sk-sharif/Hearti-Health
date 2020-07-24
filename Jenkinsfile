node(){
  stage('Cloning Git'){
    checkout scm
  }
  
  stage('Install Dependencies'){
    nodejs('nodejs'){
      sh '''npm install'''
      //echo "Modules Installed"
    }
  }
  
  stage('Build'){
    nodejs('nodejs'){
      sh 'npm run build'
      echo "Build Completed"
    }
  }
  
  stage('Package Build'){
      sh "tar -zcvf bundle.tar.gz dist/now-ui-dashboard-angular/"
  }
  
  stage('Artifacts Creation'){
      fingerprint 'bundle.tar.gz'
      archiveArtifacts 'bundle.tar.gz'
      echo "Artifacts created"
  }
  
  stage('Stash Changes'){
      stash allowEmpty: true, includes: 'bundle.tar.gz', name: 'buildArtifacts'
  }
}

node('awsnode'){
  echo 'Unstash'
  unstash 'buildArtifacts'
  echo 'Artifacts copied'
  
  echo 'Copy'
  sh "yes |  sudo cp -R bundle.tar.gz /var/www/html && cd /var/www/html && sudo tar -xvf bundle.tar.gz"
  echo 'Copy Completed'
}
