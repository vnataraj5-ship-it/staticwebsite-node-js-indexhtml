pipeline {

    agent any


    environment {
        S3_BUCKET = "staticwebsite-node-js-indexhtml"
        AWS_DEFAULT_REGION = "ap-south-1"
    }

    stages {

        stage('Checkout') {

            steps {

                git branch: 'main',
                url: 'https://github.com/vnataraj5-ship-it/staticwebsite-node-js-indexhtml.git'

            }

        }


        stage('Build') {

            steps {

                sh '''
              npm install 
              npm build 
            
                  '''

            }

        }

        stage('Deploy to S3') {
            steps {
                withCredentials([
                    [$class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-s3-creds']
                ]) {

                    sh '''
                    aws s3 sync dist/ s3://$S3_BUCKET --delete
                    '''
                }
            }
        }
    }
}

              
              





              
