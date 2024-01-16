pipeline{
    agent any
    environment{
        registry = "677168019264.dkr.ecr.ap-south-1.amazonaws.com/my-docker-repo"
    }
    stages{
        stage("checkout"){
            steps{
             checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url:[[url: 'https://github.com/kulkarni8888/myPythonDockerRepo.git']])

            }
        }
        stage("Docker Build"){
            steps{
                script{
                     dockerImage = docker.build registry
                }
                
            }
        }
        
        stage("Docker Push"){
            steps{
                script{
                    sh 'aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 677168019264.dkr.ecr.ap-south-1.amazonaws.com'
                    sh 'docker push 677168019264.dkr.ecr.ap-south-1.amazonaws.com/my-docker-repo:latest'
                }
            }
            
          }
                 stage('Docker Run'){
                steps{
                    script{
                        sh 'docker run -d -p 8096:5000 --rm --name mypythonContainer 677168019264.dkr.ecr.ap-south-1.amazonaws.com/my-docker-repo:latest'                                                                                                                                                          
                }
            }
        }
    }
}
