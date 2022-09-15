pipeline {
    agent any

    stages {
        stage('CI') {
            steps {
                sh 'zip -r siva-$BUILD_NUMBER.zip *'
                sh 'aws s3 cp siva-$BUILD_NUMBER.zip s3://artifactory-cicd-siva/'
            }
        }
        stage('CD') {
            steps {
                sh 'rm -fr *'
                sh 'aws s3 cp s3://artifactory-cicd-siva/siva-$PKG.zip .'
                sh 'unzip siva-$PKG.zip'
                sh 'scp index.html root@172.31.36.60:/var/www/html/'
            }
        }
    }
}

