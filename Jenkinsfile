 pipeline {
    agent any
    stages {

        stage('Cloning Github Repo') {
            steps {
                sh 'rm -rf DecOps_project'
                sh 'git clone https://github.com/hemanth2526/DevOps_project.git'
            }
        }

        stage('Build docker Image') {
            steps {
                sh 'cd /var/lib/jenkins/workspace/pipeline2/DevOps_project'
                sh 'cp /var/lib/jenkins/workspace/pipeline2/DevOps_project /var/lib/jenkins/workspace/pipeline2'
                sh 'cd /var/lib/jenkins/workspace/pipeline2'
                sh 'docker build -t hemanth2526/pipelinetestprod:${BUILD_NUMBER} . '
            }
        }

        stage('Push Image to docker Hub') {
            steps{
                sh 'docker push hemanth2526/pipelinetestprod:{BUILD_NUMBER}'
            }
        }

        stage('deploy to docker host'){
            steps{
                sh 'docker -H tcp://10.1.1.200:2375 run --rm -dit --name prodweb1 --hostname prodweb1 -p 9000:80 hemanth2526/pipelinetestprod:${BUILD_NUMBER}'
            }
        }
    }
}
