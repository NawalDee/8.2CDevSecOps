pipeline {
  agent any
  tools {
  nodejs "Node18"
}

  environment {
    SONAR_TOKEN = credentials('SONAR_TOKEN')
  }
  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/NawalDee/8.2CDevSecOps.git'
      }
    }
    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }
    stage('Run Tests') {
      steps {
        sh 'npm test || true'
      }
    }
    stage('Generate Coverage Report') {
      steps {
        sh 'npm run coverage || true'
      }
    }
    stage('NPM Audit (Security Scan)') {
      steps {
        sh 'npm audit || true'
      }
    }
    stage('SonarCloud Analysis') {
      steps {
        sh '''
          wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-5.0.1.3006-linux.zip
          unzip sonar-scanner-cli-5.0.1.3006-linux.zip
          ./sonar-scanner-5.0.1.3006-linux/bin/sonar-scanner
        '''
      }
    }
    stage('Deploy to Staging') {
      steps {
        echo 'Deploying to staging server...'
      }
    }
    stage('Integration Tests on Staging') {
      steps {
        echo 'Running integration tests on staging...'
      }
    }
    stage('Deploy to Production') {
      steps {
        echo 'Deploying to production server...'
      }
    }
  }
}
