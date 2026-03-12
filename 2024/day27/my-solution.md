# Answer Day 27


# Task-01

- Create a docker-integrated Jenkins declarative pipeline
- Use the above-given syntax using `sh` inside the stage block
- You will face errors in case of running a job twice, as the docker container will be already created, so for that do task 2

Answer : 
Pipeline 

pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                echo "Cloning Repository"
                git 'https://github.com/TusharDamare/node-todo-cicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker Image"
                sh 'docker build . -t trainwithshubham/node-app:latest'
            }
        }

        stage('Run Docker Container') {
            steps {
                echo "Running Docker Container"
                sh 'docker run -d -p 8000:8000 trainwithshubham/node-app:latest'
            }
        }

        stage('Verify Container') {
            steps {
                echo "Checking Running Containers"
                sh 'docker ps'
            }
        }

    }
}


# Task-02

- Create a docker-integrated Jenkins declarative pipeline using the `docker` groovy syntax inside the stage block.
- You won't face errors, you can Follow [this documentation](https://tempora-mutantur.github.io/jenkins.io/github_pages_test/doc/book/pipeline/docker/)

- Complete your previous projects using this Declarative pipeline approach


Answer : 

Pipeline 

pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git 'https://github.com/TusharDamare/node-todo-cicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("trainwithshubham/node-app:latest")
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    docker.image("trainwithshubham/node-app:latest").run("-p 8000:8000")
                }
            }
        }

        stage('Verify Container') {
            steps {
                sh 'docker ps'
            }
        }

    }
}