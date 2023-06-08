pipeline{
    agent any
    
    stages{
        stage('Cloning Git Repository'){
            steps{
                git url: "https://github.com/kamranzaidi-devops/react_django_demo_app.git", branch:'main'
            }
        }
        stage('Building Docker Image | Tagging It | Pushing Docker Image To DockerHub Registory'){
            steps{
                script{
                    def imageTag = "${env.BUILD_NUMBER}-${env.GIT_COMMIT}"
                    def imageName = "kamzaidi/jenkins_dockerhub:${imageTag}" 
                    sh "docker build -t ${imageName} ."
                    withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUsername')]){
                     sh "docker login -u ${env.dockerHubUsername} -p ${env.dockerHubPassword}"
                     sh "docker push ${imageName}"
                    }
                }
            }
        }
        stage('Deploy'){
            steps{
                echo "Deploying"
            }
        }
    }
}
