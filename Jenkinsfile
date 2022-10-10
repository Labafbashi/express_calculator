pipeline {
//	agent {
//    docker { image 'node:14-alpine' }
//  }
  agent any
	stages {
		stage('Prebuild') {
      when{
        branch 'feature/*'
      }
      steps {
        echo "********************* FEATURE *********************"
				sh 'npm install'
			}
		}
    stage('Unit test') {
      steps {
        sh 'npm run test-unit'
      }
    }
    stage('Unit test all') {
      steps{
        sh 'npm run test-all'
      }
    }
    stage('Unit test integration'){
      when{
        anyof {
          branch 'develop';
          branch 'main'
        }
      }
      steps {
        echo "********************* DEVELOP / MAIN *********************"
        sh 'npm run test-integration'
      }
    }
  }
}
