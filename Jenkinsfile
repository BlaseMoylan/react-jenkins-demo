pipeline{
    agent any

    stages{
        stage('Build'){
            steps{
                script{
                    def nodejstool = tool name: 'node-20-tool', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
                    env.PATH = "${nodejstool}/bin:${env.PATH}"
                }
                sh '''
                    echo "Building the application..." 
                    npm install
                    npm run-script build
                 '''
            }
        }
        stage('Docker'){
            steps{
                script{
                    def dockertool = tool name: 'docker-latest-tool', type: 'org.jenkinsci.plugins.docker.commons.tools.DockerTool'
                    env.PATH = "${dockertool}/bin:${env.PATH}"
                }
                sh '''
                echo "Dockerizing the application..."
                docker build -t blasemoylan/react-jenkins-docker:latest .
                '''
                // withcredentials
                // push
                withCredentials([usernamePassword(credentialsId: 'personal-docker-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                // Use the USERNAME and PASSWORD environment variables are available within this block  
                            sh 'docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}'
                }

                        // Now that we have logged in with the credentials above, we can do authenticated actions like pushing
                // sh "docker push <SOME IMAGE NAME>"
                    }
        }
        // stage('Build'){
        //     steps{
        //         sh 'echo "Building the application..." '
        //     }
        // }
    }
}