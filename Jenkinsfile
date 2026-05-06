pipeline {
    agent { label "Pankaj" }
    
    stages {
        stage("Code") {
            steps {
                echo "This is cloning the code"
                git url: "https://github.com/Raghunandan-79/Notes-App.git", branch: "main"
                echo "Code cloning successful"
            }
        }
        stage("Build") {
            steps {
                echo "This is building the code"
                sh "docker build -t notes-app:latest ."
                echo "Build successfull"
            }
        }
        stage("Push to DockerHub") {
            steps {
                echo "This is pushing image to dockerhub"
                withCredentials([usernamePassword(
                    'credentialsId': "dockerHubCred",
                    passwordVariable: "dockerHubPass",
                    usernameVariable: "dockerHubUser"
                )]) {
                    sh "docker login -u ${env.dockerHubUser} -p ${dockerHubPass}"
                    sh "docker image tag notes-app:latest ${env.dockerHubUser}/notes-app:latest"
                    sh "docker push ${env.dockerHubUser}/notes-app:latest"
                }
            }   
        }
        stage('Deploy') {
            steps {
                echo "Deploying application"
        
                sh 'docker compose down || true'
        
                sh 'docker compose up -d --build'
            }
        }
    }
}
