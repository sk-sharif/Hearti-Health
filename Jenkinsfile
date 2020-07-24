pipeline{
  agent any
  stages{
    stage('Install Dependencies'){
      steps{
          nodejs('nodejs'){
          sh 'npm install'
          echo "Modules Installed"
        }
      }
    }
    
    stage('Build'){
      steps{
        nodejs('nodejs'){
          sh 'npm run build'
          echo "Build Completed"
        }
      }
    }
    
  }
}
