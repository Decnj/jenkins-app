pipeline {
    agent {
        docker {
            image 'ubuntu:noble'
            args '-u root'
            reuseNode true
        }
    }

    stages {
        stage('Update Package') {
            steps {
                sh '''
                    apt-get update -y
                '''
            }
        }

        stage('Install Apache') {
            steps {
                sh '''
                    apt-get install -y apache2
                '''
            }
        }

        stage('Setup Apache runtime dir') {
            steps {
                sh '''
                    mkdir -p /var/run/apache2
                    chown wwww-data:www-data /var/run/apache2
                    echo "export APACHE_RUN_DIR=/var/run/apache2" >> /etc/apache2/envvars
                    echo "export APACHE_LOG_DIR=/var/log/apache2" >> /etc/apache2/envvars
                    echo "ServerName localhost" >> /etc/apache2/apache2.conf
                '''
            }
        }

        stage('Verify Installation') {
            steps {
                sh'''
                    apache2ctl -V
                '''
            }
        }

        stage('Start Apache2') {
            steps {
                sh '''
                    apache2ctl -D FOREGROUND &
                '''
            }
        }
    }
}