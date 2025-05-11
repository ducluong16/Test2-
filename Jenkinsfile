pipeline {
    agent any
    tools {
        maven
    }
    stages {
        stage("build jar"){
            steps{
                script {
                    echo 'building the application'
                    sh 'mvn package'
                }
            }
        }

        stage("build image"){
            steps{
                script{
                    echo 'building the image...'
                    withCredentials([
                        usernamePassword(
                            credentialsId: 'Docker_Hub'
                            usernameVariable: 'USERNAME'
                            passwordVariable: 'PWD'
                        )
                    ]){
                        sh 'docker build -t ducluong16/luongpham:3.0 .'
                        sh "echo $PWD | docker login -u $USERNAME --password-stdin"
                        sh 'docker push ducluong16/luongpham:3.0'
                    }
                }
            }
        }
    }   
}
