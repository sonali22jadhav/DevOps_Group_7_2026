pipeline {
    agent any

    stages {
        stage('First Step') {
            steps {
                sh 'sudo yum install httpd -y'
            }
        }

        stage('Second Step') {
            steps {
                sh 'sudo service httpd start'
                sh 'echo "Hello world" | sudo tee -a /var/www/html/index.html'
                sh 'sudo chmod -R 777 /var/www/html'
            }
        }
    }
}
