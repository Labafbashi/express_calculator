pipeline {
//	agent {
//    docker { image 'node:14-alpine' }
//  }
  agent any
	stages {
		stage('Prebuild') {
// For Develop stage we couldn't use this section. because we need 'npm install' before next steps.
//      when{
//        branch 'feature/*'
//      }
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
        anyOf {
          branch 'develop';
          branch 'main'
        }
      }
      steps {
        echo "********************* DEVELOP / MAIN *********************"
        sh 'npm run test-integration'
      }
    }
    stage('Delivery'){
      when{
        branch 'main'
      }
      steps {
        docker.withRegistery('https://registery.hub.docker.com', 'dockerhub') {
          def img = docker.build("paramont/express-calculator")
          img.push()
        }
      }
    }
  }
}
