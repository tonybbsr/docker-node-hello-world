pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3"
    }

    stages {
        stage('Git Pull') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/tonybbsr/hello-world.git'
            }
        }
        stage('Maven Build') {
            steps {
                // Get some code from a GitHub repository
                sh 'mvn install package'
            }
        }
        
         stage('Docker Build') {
            steps {
                // Get some code from a GitHub repository
                sh 'sudo docker build -t tonybbsr/debasis:${BUILD_NUMBER} .'
            }
        }
        stage('Docker push to docker hub') {
            steps {
                // Get some code from a GitHub repository
                sh 'sudo docker login -u tonybbsr -p Grt@12345'
                sh 'sudo docker push tonybbsr/debasis:${BUILD_NUMBER}'
            }
        }
         stage('Docker run ') {
            steps {
                // Get some code from a GitHub repository
                sh 'sudo docker stop Mohanty'
                sh 'sudo docker rm Mohanty'
                sh 'sudo docker run -itd -p 8082:8080 --name Mohanty tonybbsr/debasis:${BUILD_NUMBER}'
            }
        }
//         stage('Deploy To Tomcat') {
//             steps {
//                 // Get some code from a GitHub repository
//                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://34.125.237.227:8080/')], contextPath: null, war: 'webapp/target/webapp.war'
//             }
//         }
    }
}
