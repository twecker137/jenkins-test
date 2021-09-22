pipeline {
    agent any

    options {
      buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '30', numToKeepStr: '30')
    }

    stages {
      stage('Git') {
        steps {
          sh "date > date.txt"
          sh 'git config --global user.email "twecker@bright-skies.de"'
          sh 'git config --global user.name "Tony Wecker (Jenkins)"'

          sh "git add date.txt"
          sh 'git commit -m "changed date"'

          withCredentials([usernamePassword(credentialsId: 'github-towe-jenkins-test', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
              sh 'git config remote.origin.url https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/twecker137/jenkins-test.git'
          }

          sh "git push origin main"
        }
      }
    }
}