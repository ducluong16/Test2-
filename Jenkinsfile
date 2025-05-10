pipeline {
  agent any
  tools {
    maven 'Maven'
  }
  stages {
    stage("build jar") {
      steps {
        script {
          echo 'building the application...'
          sh 'mvn package'
        }
      }
    }
    stage("build image") {
      steps {
        script {
          echo 'building the docker image...'
          withCredentials([
            usernamePassword(credentials: 'Docker_Hub', usernameVariable: 'USERNAME', passwordVariable: 'PWD')
          ]) {
            sh 'docker build -t ducluong16/luongpham:2.0 .'
            sh "echo $PWD | docker login -u $USERNAME --password-stdin"
            sh 'docker push ducluong16/luongpham:2.0'
          }
        }
      }
    }
    stage("deploy") {
      steps {
        script {
          echo 'deploying the application...'
        }
      }
    }
  }
}
