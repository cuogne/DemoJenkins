pipeline {
  agent any

  options {
    timestamps()
  }

  environment {
    // Replace with your real GitHub repository URL.
    REPO_URL = 'https://github.com/cuogne/DemoJenkins.git'
    REPO_BRANCH = 'main'
  }
  
  triggers {
    pollSCM('H/5 * * * *')
  }
  
  stages {
    stage('Checkout') {
      steps {
        git url: "${REPO_URL}", branch: "${REPO_BRANCH}"
      }
    }

    stage('Verify Python') {
      steps {
        sh 'python3 --version'
      }
    }
    
    stage('Test') {
      steps {
        sh '''
          python3 -m unittest discover -s . -p "test_*.py" -v
        '''
      }
    }
  }

  post {
    always {
      echo 'Pipeline finished.'
    }
    success {
      echo 'All tests passed successfully.'
    }
    failure {
      echo 'Some tests failed. Please check the logs.'
    }
  }
}