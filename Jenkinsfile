pipeline {
  agent any
  environment {
    PATH = "/opt/homebrew/bin:$PATH"
  }
  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/Niethin69/8.2CDevSecOps.git'
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
  }
  post {
    always {
      emailext (
        subject: "Jenkins Build - ${currentBuild.fullDisplayName} - ${currentBuild.result}",
        body: """<p>Build Result: <b>${currentBuild.result}</b></p>
                 <p>Job: ${env.JOB_NAME}</p>
                 <p>Build Number: ${env.BUILD_NUMBER}</p>
                 <p>Build URL: <a href='${env.BUILD_URL}'>Click here</a></p>""",
        recipientProviders: [[$class: 'DevelopersRecipientProvider']],
        to: 'niethinrueshil@gmail.com',  
        attachLog: true,
        mimeType: 'text/html'
      )
    }
  }
}

