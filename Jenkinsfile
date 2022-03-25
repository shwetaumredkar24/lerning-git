pipeline {
  environment {
    imagename = "shweta1999/mynginxapp"
    registryCredential = 'dockerhubid'
    dockerImage = ''
    }
    agent any
    stages {
        stage('Git Clone') {
            steps {
                git([url: 'https://github.com/shwetaumredkar24/lerning-git.git', branch: 'master', credentialsId: 'githubid'])
            }
        }
        stage('Build Image') {
            steps {
               script {
                 dockerImage = docker.build imagename
               }
            }
        }
        stage('Deploy Image') {
            steps {
                script {
                  docker.withRegistry( '', registryCredential ) {
                    dockerImage.push("$BUILD_NUMBER")
                  }
                }
            }
        }
        stage('Remove Unused docker image') {
            steps {
              sh "docker rmi $imagename:$BUILD_NUMBER"
             }
        }
    }
}
