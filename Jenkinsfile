@Library("Shared") _
pipeline {
    agent { label  "pushit" }
    stages {
        stage("Hello"){
            steps {
                script {
                    hello()
                }
            }
        }
        stage("Code"){
            steps {
                script{
                    clone("https://github.com/pushitchaudhary/react-cicd-pipeline.git", "main")
                }
            }
        }

        stage("Build"){
            steps {
                echo "This is building the code"
                sh "whoami"
                sh "docker build -t notes-app:latest ."
            }
        }
        stage("Test"){
            steps {
                 echo "This is testing the code" 
            }
        }
        stage("Pushing to DockerHub"){
            steps {
                echo "Pushing image to the docker hub"
                script{
                    docker_push("notes-app","latest", "pushitchaudhary")
                }
                // withCredentials([
                //     usernamePassword('credentialsId':"dockerHubCred", 
                //     passwordVariable:"dockerHubPass", 
                //     usernameVariable:"dockerHubUser")]){
                //         sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass} "
                //         sh "docker image tag notes-app:latest ${env.dockerHubUser}/notes-app:latest"
                //         sh "docker push ${env.dockerHubUser}/notes-app:latest"
                // }
            }
        }
        stage("Deploy"){
            steps {
                echo "This is Deploying the code"
                sh "docker compose down && docker compose up -d"
            }
        }
    }
}