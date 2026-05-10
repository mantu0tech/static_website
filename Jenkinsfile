pipeline{
    agent any 
    environment{
        BUCK = "aws-s3-234567-sf"
    }
    stages{
        stage("clone"){
            steps{
                echo "cloning "
                sh 'aws s3 ls'
                git branch: 'main', url: 'https://github.com/mantu0tech/static_website.git'
            }
            
        }
        stage("check"){
            steps{
                echo "check if bucket is there or not  "
                sh '''
                if aws s3 ls s3://${BUCK}; then
                    echo "bucket already exist"
                else
                    echo "creating bucket...."
                    aws s3 mb s3://${BUCK}
                fi 
                '''
            }
            
        }
        stage("deply"){
            steps{
                echo "sync to s3 bucket  "
                sh 'aws s3 sync . s3://${BUCK}/'
            }
            
        }
    }
    post{
        always {
            echo "it will run always "
        }
        failure {
            echo "pipeline got filed "
        }
        success {
            echo "creating the artifact "
            sh 'tar -cvf demo.tar index.html '
            
        }
    }
    
}
