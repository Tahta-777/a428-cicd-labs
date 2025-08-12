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
	stage("Deploy")
		steps {
			sh './jenkins/script/deliver.sh'
			input message: 'Sudah selesai menggunakan React App? (klik "Proceed" untuk mengakhiri)'
			SH './jenkins/scripts/kill.sh'
	}
}
