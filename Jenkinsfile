pipeline {
  agent {
    docker {
      image 'node:18'
      args '-p 3000:3000'
    }
  }

  environment {
    NODE_OPTIONS = '--openssl-legacy-provider'
  }

  stages {
    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('Build') {
      steps {
        sh 'npm run build'
      }
    }

    stage('Serve') {
      steps {
        // Install serve locally
        sh 'npm install serve'

        // Start server
        sh 'npx serve -s build -l 3000 &'
        sh 'sleep 10'
      }
    }

    stage('Test') {
      steps {
        sh 'curl -I http://localhost:3000'
      }
    }
  }

  post {
    always {
      sh 'echo "Pipeline completed"'
    }
  }
}
