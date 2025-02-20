 
pipeline {
    agent any

    environment {
        JACOCO_COVERAGE_DIR = "target/site/jacoco"
    }

    triggers {
        cron('H/3 * * * 4') // Runs every 3 minutes on Thursdays
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/YOUR_GITHUB_USERNAME/spring-petclinic.git'
            }
        }

        stage('Build') {
            steps {
                sh './mvnw clean install'
            }
        }

        stage('Code Coverage with JaCoCo') {
            steps {
                sh './mvnw jacoco:report'
            }
            post {
                success {
                    publishHTML([
                        reportDir: "${JACOCO_COVERAGE_DIR}",
                        reportFiles: 'index.html',
                        reportName: 'JaCoCo Coverage Report'
                    ])
                }
            }
        }
    }
}
