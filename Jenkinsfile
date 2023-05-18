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
                    def dockertool = name: 'docker-latest-tool', type: 'org.jenkinsci.plugins.docker.commons.tools.DockerTool'
                    env.PATH = "${dockertool}/bin:${env.PATH}"
                }
                sh 'echo "Dockerizing the application..." '
                
            }
        }
        // stage('Build'){
        //     steps{
        //         sh 'echo "Building the application..." '
        //     }
        // }
    }
}