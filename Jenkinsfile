pipeline {
    agent any
    parameters {
        booleanParam(name: 'TEST_PROJECT',defaultValue: true)
    }
    stages {
        stage("Checkout") {
            steps {
                git url: "https://github.com/ZooLeeCoding/Spring-Devops.git"
            }
        }
        stage("Compile") {
            steps {
                sh "./gradlew compileJava"
            }
        }
        stage("Unit Test") {
            when { expression { return params.TEST_PROJECT } }
            steps {
                sh "./gradlew test"
            }
        }
    }
}