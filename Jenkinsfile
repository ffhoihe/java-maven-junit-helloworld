pipeline {
  agent any
  stages {
    stage('checkout project') {
      steps {
        checkout scm
        git ' java-maven-junit-helloworld '
      }
    }

    stage('build') {
      steps {
        sh 'mvn clean package'
      }
    }

    stage('archive') {
      parallel {
        stage('archive') {
          steps {
            archiveArtifacts 'target/*jar'
          }
        }

        stage('junit') {
          steps {
            junit '**/target/surefire-reports/TEST-*.xml'
          }
        }

      }
    }

  }
}