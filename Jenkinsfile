pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('sonar-token')
        DOCKERHUB_CREDS = credentials('dockerhub-creds')
        NEXUS_CREDS = credentials('nexus-creds')
    }

    stages {
        stage('Build') {
            steps {
                sh './mvnw clean package -DskipTests'
            }
        }

        stage('SonarQube Scan') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh './mvnw sonar:sonar'
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t employee-management-system:latest .'
            }
        }

        stage('Trivy Scan') {
            steps {
                sh '''
                    trivy image employee-management-system:latest \
                    --format json \
                    --output trivy-report.json || true
                '''
                archiveArtifacts artifacts: 'trivy-report.json', fingerprint: true
            }
        }

        stage('Publish to Nexus') {
            steps {
                sh './mvnw deploy'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                    kubectl apply -f k8s/deployment.yaml
                    kubectl apply -f k8s/service.yaml
                '''
            }
        }
    }
}
