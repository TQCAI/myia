node ('gpu') {
  stage ('Checkout') {
    checkout scm
  }
  stage ('Install') {
    sh script: './ci-install.sh --gpu'
  }
  stage ('Test') {
    sh script: '$HOME/miniconda/bin/pytest --cov-report=term-missing --cov-report=xml  --cov=./ --gpu --junit-xml test-report.xml'
    junit 'test-report.xml'
  }
  stage ('Coverage') {
    withCredentials([string(credentialsId: 'myia_codecov', variable: 'CODECOV_TOKEN')]) {
      sh script: 'curl -s https://codecov.io/bash | bash -s -- -ZK'
    }
  }
}
