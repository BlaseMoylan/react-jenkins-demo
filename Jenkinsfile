pipeline{
    agent any

    stages{
        stage('Build'){
            steps{
                script{
                    def nodejstool = tool name: 'node-20-tool', type: 'jenkins.plugins.nodejs.tools.NodeJSInstillation'
                    env.PATH = "${nodejstool}/bin:${env.PATH}"
                }
                sh 'echo "Building the application..." '
                sh 'npm install'
            }
        }
        stage('Docker'){
            steps{
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