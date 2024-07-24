pipeline {
    agent any
    enviroment {
        DOCKER_CREDENTIALS_ID = 'dockerhub-credentials-id'
        DOCKER_IMAGE = 'uqlutzavr/web-sql'

    }
    stages{
        stage('Clone repository'){
            steps{
                git branch: 'main', url: 'https://github.com/uqlutzavr/web-sql'
            }

    }
        stage('Build Dockerimage'){
            steps{
                script{
                    docker.build(DOCKER_IMAGE)
                }
            }
        
    }
        stage('Run tests'){
            steps{
                sh echo 'Tests...'
            }
        
    }
        stage('Push to dockerhub'){
            when {
                expression {currentBuild.currentResult == 'SUCCESS'}
            }
            steps{
                script{
                    docker.withRegistry('https://index.docker.io/v1', DOCKER_CREDENTIALS_ID){
                        docker.image(DOCKER_IMAGE).push
                    }
                }
            }
        
    }
        post {
            failer {
                echo "Build or test failed"
            }
        }
    }
}