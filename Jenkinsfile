pipeline{
    environment{
        registry = "reshmababu/demoimage"
        registryCredential = 'docker_hub_id'
        dockerImage=''
    }
    agent any
    stages {
        stage('cloning git'){
            steps {
                git ([url: 'https://github.com/Reshu1123/jenkinstotomcatPipeline.git',branch: 'main', credentialsId: 'github_id'])

            }
        }
        stage('Building image'){
            steps{
                script{
                     dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Deploying image'){
            steps{
                sh "docker run -d $registry:$BUILD_NUMBER"
                script{
                    docker.withRegistry('',registryCredential){
                        dockerImage.push()
                    }
                }
            }
        }
        stage('cleaning up'){
            steps{
                sh "docker rmi $registry:$BUILD_NUMBER"
            }
        }
    }
}
