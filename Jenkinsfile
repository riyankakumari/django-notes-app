@Library("shared") _
pipeline {
    agent { label "riyanka" }

    stages {
        stage("Hello"){
            steps{
                script{
                    hello()
                }
            }
        }

        stage("Code") {
            steps {
                echo "This is cloning the code"
                script{
                    gitClone ("https://github.com/riyankakumari/django-notes-app","main")
                }
                echo "code cloning successfull"
            }
        }

       stage("Build") {
            steps {
            echo "building the image"
                 script {
                     build("notes-app", "latest", "riyankakumari")
                 }
              }
        }

        stage("push to docker hub") {
            steps {
                script {
                    pushDockerImage("notes-app", "latest", "riyankakumari")
                }
            }
        }

        stage("Test") {
            steps {
                echo "Testing the code"
            }
        }

       stage("Deploy") {
    steps {
        echo "Deploying the code"
        sh "docker compose down && docker compose up -d "
        // script{
        //     deploy()
        // }
    }
}
        

    }
}
