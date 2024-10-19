pipeline {
    agent any
    stages {
        stage('Build Blue') {
            steps {
                script {
                    bat 'docker build -t django-app:blue .'
                    bat 'kubectl apply -f blue-deployment.yaml'
                }
            }
        }
        stage('Deploy Green') {
            steps {
                script {
                    bat 'docker build -t django-app:green .'
                    bat 'kubectl apply -f green-deployment.yaml'
                }
            }
        }
        stage('Test Green') {
            steps {
                script {
                    // Perform testing or health checks on green environment
                }
            }
        }
        stage('Switch Traffic to Green') {
            steps {
                script {
                    bat 'kubectl patch service django-app-service -p \'{"spec": {"selector": {"version": "green"}}}\''
                }
            }
        }
        stage('Cleanup Blue') {
            steps {
                script {
                    bat 'kubectl delete deployment blue-deployment'
                }
            }
        }
    }
}
