pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        deleteDir()
        git 'https://github.com/pavel-snyk/multimodule-js-goof'
      }
    }
    stage('Security') {
      steps {
        try {
          snykSecurity monitorProjectOnBuild: false,
                       snykInstallation: 'snyk@latest',
                       snykTokenId: 'pavel-snyk-token',
                       failOnIssues: false
        } catch (Exception ex) {
          echo "Snyk Scan Failed"
          currentBuild.result='FAILURE'
          error e.toString()
        } 
      }
    }
  }
}
