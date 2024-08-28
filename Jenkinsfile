pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                // Tool: Maven
                // Example command: mvn clean package
                script {
                    sh 'mvn clean package'
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                // Tools: JUnit (for unit tests), TestNG (for integration tests)
                // Example command: mvn test
                script {
                    sh 'mvn test'
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code...'
                // Tool: SonarQube
                // Example command: mvn sonar:sonar
                script {
                    sh 'mvn sonar:sonar'
                }
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                // Tool: OWASP Dependency-Check
                // Example command: dependency-check --project MyProject
                script {
                    sh 'dependency-check --project MyProject'
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging...'
                // Tool: AWS CLI
                // Example command: aws deploy create-deployment --application-name MyApp --deployment-group-name Staging
                script {
                    sh 'aws deploy create-deployment --application-name MyApp --deployment-group-name Staging'
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Tool: Selenium
                // Example command: mvn verify
                script {
                    sh 'mvn verify'
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                // Tool: AWS CLI
                // Example command: aws deploy create-deployment --application-name MyApp --deployment-group-name Production
                script {
                    sh 'aws deploy create-deployment --application-name MyApp --deployment-group-name Production'
                }
            }
        }
    }
    post {
        success {
            emailext (
                to: 'roji13804@gmail.com',
                subject: "Build Successful: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build was successful.\n\nCheck console output for details: ${env.BUILD_URL}",
                attachLog: true
            )
        }
        failure {
            emailext (
                to: 'roji13804@gmail.com',
                subject: "Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build failed.\n\nCheck console output for details: ${env.BUILD_URL}",
                attachLog: true
            )
        }
    }
}
