pipeline {
    agent any
    stages {
        stage("Checkout") {
            steps {
                git url: "https://github.com/vinczea/Spring-Devops.git"
            }
        }
        stage("Packaging") {
            steps {
                sh "./gradlew build"
            }
        }
        stage("Docker build") {
            steps {
                sh "docker build -t vinczea/devops-pelda ."
            }
        }
        stage("Docker login") {
            steps {
                sh "docker login --username=vinczea --password=$docker_password"
            }
        }
        stage("Docker push") {
            steps {
                sh "docker push vinczea/devops-pelda"
            }
        }
        stage("Deploy to Staging") {
            steps {
                sh "docker run -d --rm -p 8765:8080 --name calculator vinczea/devops-pelda"
            }
        }
        stage("Acceptance Test") {
            steps {
                sh "sleep 60"
                sh "./acceptance_test.sh"
            }
        }
    }
    post {
        always {
            sh "docker stop calculator"
        }
    }
}
