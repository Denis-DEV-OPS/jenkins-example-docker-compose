pipeline {
  agent any
  stages {
    stage("verify tooling") {
      steps {
        sh '''
          docker version
          docker info
          docker-compose --version 
          curl --version
        '''
      }
    }
    stage('Prune Docker data') {
      steps {
        sh 'docker system prune --volumes -f'
      }
    }
    stage('Start container') {
      steps {
        sh 'sudo docker-compose up -d'
        sh 'sudo docker-compose ps'
      }
    }
    stage('Run tests against the container') {
      steps {
        sh 'curl http://localhost:3000/param?query=demo'
      }
    }
  }
  post {
    always {
      sh 'sudo docker-compose down --remove-orphans -v'
      sh 'sudo docker-compose ps'
    }
  }
}
