@Library("shared") _
pipeline{
    agent {label "dev"}
    
    stages{
        stage("code"){
            steps{
                script{
                    clone("https://github.com/tauseefkhorajia/django-notes-app.git", "main")
                }
            }
        }
        stage("build"){
            steps{
                sh "docker build -t django-notes-app ."
            }
        }
        stage("test"){
            steps{
                echo "devloper test likhega"
            }
        }
        stage("push-to-dockerHub"){
            steps{
                script{
                    docker_push("dockerHubCred", "django-notes-app")
                }
            }
        }
        stage("deploy"){
            steps{
                sh "docker compose up -d"
            }
        }
    }

post{
    success{
            script{
                emailext from: 'tosifkhorajia@gmail.com',
                to: 'tosifkhorajia@gmail.com',
                body: 'Build success for Demo CICD App',
                subject: 'Build success for Demo CICD App'
            }
        }
        failure{
            script{
                emailext from: 'tosifkhorajia@gmail.com',
                to: 'tosifkhorajia@gmail.com',
                body: 'Build Failed for Demo CICD App',
                subject: 'Build Failed for Demo CICD App'
            }
        }
}

    
}
