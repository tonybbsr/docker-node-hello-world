pipeline {
    agent any

    stages {
        stage('Git Pull') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/tonybbsr/docker-node-hello-world.git'
            }
        }
    stage('Docker Build') {
            steps {
                // Get some code from a GitHub repository
                sh 'sudo docker build -t tonybbsr/demo:${BUILD_NUMBER} .'
            }
        }
        stage('Docker push to docker hub') {
          steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                    sh 'docker push tonybbsr/demo:${BUILD_NUMBER}'
                }
          }
     }
         stage('Docker run ') {
            steps {
                // Get some code from a GitHub repository
                sh 'sudo docker stop Demo'
                sh 'sudo docker rm Demo'
                sh 'sudo docker run -itd -p 8082:4000 --name Demo tonybbsr/demo:${BUILD_NUMBER}'
            }
        }
       stage('Trigger ManifestUpdate') {
            steps {
                echo "triggering updatemanifestjob"
                build job: 'updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
            }
        }
    }
}
