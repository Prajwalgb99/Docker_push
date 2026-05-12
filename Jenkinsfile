pipeline {
    agent any

    environment {
        // ID of the credentials stored in Jenkins
        DOCKER_CREDENTIAL_ID = "Docker" 
        // Full repository name on DockerHub
        IMAGE_NAME = "iamprajwal99/docker_image"
    }

    stages {
        stage('Build Java Application') {
            steps {
                bat "javac HelloWorld.java"
            }
        }

        stage('Run Java Program') {
            steps {
                bat "java HelloWorld"
            }
        }

        stage('Build Docker Image') {
            steps {
                // Use the variable defined in the environment block
                bat "docker build -t %IMAGE_NAME%:latest ."
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: "Docker" ,
                    usernameVariable: "USER",
                    passwordVariable: "PASS"
                )]) {
                    // Windows batch command to login
                    bat "docker login -u %USER% -p %PASS%"
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                bat "docker push %IMAGE_NAME%:latest"
            }
        }
    }
    
    post {
        always {
            // Good practice to logout after pushing
            bat "docker logout"
        }
    }
}






// First create a folder and write these files after that sign in for docker hub open jenkins go to settings credentials add credentials , username and pass word (of docker) model name as Docker and click create 
// click on item , enter item name select pipeline click ok 
// Next go to pipeline select pipeline from scm scm ->git , repo url 
// change master to main 
// Choose script path to jenkinsfile

// build pipelen(if erreo comes check for plugin) Pipeline , Git , Credentials Binding , Docker Pipeline ,Blue Ocean , Docker Commons
