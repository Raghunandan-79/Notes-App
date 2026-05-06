@Library("Shared") _
pipeline {
    agent { label "worker" }
    
    stages {
        stage("Code") {
            steps {
                script {
                    git_clone("https://github.com/Raghunandan-79/Notes-App.git", "main")
                }
            }
        }
        stage("Build") {
            steps {
                docker_build("notes-app", "latest", "raghunandan79")
            }
        }
        stage("Push to DockerHub") {
            steps {
                script {
                    docker_push("notes-app", "latest", "raghunandan79")
                }
            }   
        }
        stage('Deploy') {
            steps {
                sh 'docker compose down && docker compose up -d'
            }
        }
    }
}
