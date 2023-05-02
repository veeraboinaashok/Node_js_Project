pipeline{
    agent any
    stages{
        stage('checkout code'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/veeraboinaashok/Node_js_Project']])
            }
        }
        stage('build maven')
        stage('Build mvn'){
            steps{
             script{
                 sh 'mvn clean package'
             }   
            }
        }
        stage('docker image build')
        stage('Build docker image'){
            steps{
             script{
                 sh 'docker build -t images:2.0 .'
             }   
            }
        }
        stage('create docker container'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub')]){
                        sh 'docker login -u veeraboinaashok0124 -p ${dockerhub}'
                    }
                       sh 'docker tag images:2.0 veeraboinaashok0124/nodejs:2.0'
                       sh 'docker push veeraboinaashok0124/nodejs:2.0'
                       sh 'docker container run -d -p 3000:3000 images:2.0 npm run start'
                }
            }
        }
    }
}
