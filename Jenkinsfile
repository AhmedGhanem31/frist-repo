pipeline {
    agent any

    stages {
        stage('build') 
        {
            steps {
                git branch: 'main', url: 'https://github.com/AhmedGhanem31/frist-repo.git'
                sh "docker build -t ahmedghanem1/web-app:${env.BUILD_ID} ."
                withCredentials([usernamePassword(credentialsId: 'docker-cre', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                  
                                    sh "docker login -u $USERNAME -p $PASSWORD"

                }
                sh "docker push ahmedghanem1/web-app:${env.BUILD_ID}"
            }
        }
        stage('deploy')
        {
            steps{
                sh "docker stop webapp"
                sh "docker rm webapp"
                sh "docker run -itd -p 8085:80 --name webapp ahmedghanem1/web-app:${env.BUILD_ID}"
            }
        }

    }
}
