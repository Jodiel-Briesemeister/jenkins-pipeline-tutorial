pipeline {
  agent {
    label 'maven'
  }

  parameters {
    booleanParam(name: 'CLEAN_BEFORE_BUILD', description: 'Limpar o workspace antes de rodar o build')
  }

  stages {
    stage('Clean') {
      when {
        expression { params.CLEAN_BEFORE_BUILD }
      }

      steps {
        sh 'mvn clean'
      }
    }

    stage('Compile') {
      steps {
        sh 'mvn compile'
      }
    }

    stage('Test') {
      steps {
        sh 'mvn verify'
      }
    }

    stage('Deploy') {
      steps {
        script {
          def pom = readMavenPom file: 'pom.xml'
          sh "./deploy.sh ${pom.getArtifactId()} ${pom.getVersion()}"
        }
      }
    }
  }
}