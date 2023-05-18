pipeline{
    agent any
    environment {
        def nodejstool = tool name: 'node-20-tool', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
        def dockertool = tool name: 'docker-latest-tool', type: 'org.jenkinsci.plugins.docker.commons.tools.DockerTool'
        PATH = "${nodejstool}/bin:${dockertool}/bin:${env.PATH}"

    }
    stages{
        stage('Install Dependencies'){
            steps{
                
                sh 'npm install'
            }
        }
        stage('Create Production Build'){
            steps{
                
                sh 'npm run-script build'
            }
        }
        stage('Build Docker Image'){
            steps{
                
                sh 'docker build -t --name=blasemoylan/react-jenkins blasemoylan/react-jenkins-docker:latest .'
        }
        stage('Push Docker Image'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'personal-docker-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                // Use the USERNAME and PASSWORD environment variables are available within this block  
                            sh 'docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}'
                }

                        // Now that we have logged in with the credentials above, we can do authenticated actions like pushing
                sh "docker push blasemoylan/react-jenkins"
                    }
        }
        
    }
}
}
