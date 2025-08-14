@Library("Shared") _
pipeline {
    agent { label "vinod" }

    stages {
        stage("Hello") {
            steps {
                script {
                    hello()
                }
            }
        }

        stage("Clone Code") {
            steps {
                script {
                    clone("https://github.com/zaidu000/two-tier-flask-app.git", "main")
                }
            }
        }

        stage("Build Docker Image") {
            steps {
                script {
                    build("notes-app", "latest", "zaidu000")
                }
            }
        }

        stage("Push to Docker Hub") {
            steps {
                script {
                    push(
                        imageName: "zaidu000/notes-app",
                        imageTag: "latest",
                        credentials: "DockerHubCred"
                    )
                }
            }
        }

        stage("Deploy") {
            steps {
                echo "Deploying container with DB environment variables..."
                sh "docker compose up -d"
            }
        }
    }
}
