pipeline {
    agent none

    stages {

        stage('Build') {
            agent {
                label 'node-a'
            }
            steps {
                echo "Running Build on Node A"
                sh 'hostname'
                sh 'sleep 10'
            }
        }

        stage('Unit Test') {
            agent {
                label 'node-b'
            }
            steps {
                echo "Running Unit Test on Node B"
                sh 'hostname'
                sh 'sleep 10'
            }
        }

        stage('Parallel Execution') {
            parallel {

                stage('Integration Test') {
                    agent {
                        label 'node-c'
                    }
                    steps {
                        echo "Running Integration Test on Node C"
                        sh 'hostname'
                        sh 'sleep 20'
                    }
                }

                stage('Security Scan') {
                    agent {
                        label 'node-d'
                    }
                    steps {
                        echo "Running Security Scan on Node D"
                        sh 'hostname'
                        sh 'sleep 20'
                    }
                }
            }
        }

        stage('Deploy') {
            agent {
                label 'node-e'
            }
            steps {
                echo "Deploying after all parallel stages complete"
                sh 'hostname'
            }
        }
    }

    post {
        always {
            echo "Pipeline Completed"
        }
        success {
            echo "Pipeline Success"
        }
        failure {
            echo "Pipeline Failed"
        }
    }
}
