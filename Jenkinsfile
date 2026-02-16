pipeline{
    agent any
    triggers{
        pollSCM{'* * * * *'}
    }
    stages{
        stage('checkout'){
            steps{
                git url:'https://github.com/Naresh1770/flask-cicd-app.git',
                    branch: 'master'
            }
        }
        stage('Reuired Dependencies'){
            steps{
                sh 'pip install -r requirements.txt'
            }
        }
        stage('Test'){
            steps{
                sh 'pytest'
            }
        }
        stage('Docker Build Image'){
            steps{
                sh 'docker image build -t naresh1770/flask-cicd:latest .'
            }
        }
        stage('Docker Push'){
            steps{
                sh '''
                   docker login -u naresh1770 -p Naresh@1770
                   doccker push naresh1770/flask-cicd:latest
                '''
            }
        }
        stage('Deploy'){
            steps{
                sh '''
                   docker rm -f flask-cicd || true
                   docker run -d -p 5000:5000 --name flask naresh1770/flask-cicd:latest
                '''
            }
        }
    }
    post{
        success{
            echo'Pipeline is completed successfully'
        }
        failure{
            echo'Pipeline is failed'
        }
    }
}